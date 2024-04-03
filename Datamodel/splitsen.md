### Splitsfunctie in hoofdquery:
```sql
  , stp_adf_rapport.set_splitsen(
            p_referentie_id              => <tabel.veld_id> -- ID veld waarop gesplitst/afgeleverd wordt
            , p_referentietabel          => <referentietabel> 
            ,  p_bestandsnaam            => oss_adf_utility.bestandsnaam(
                                                 p_bestandsnaam => 
                                                     -- Eerst wordt de koppelsleutel gemaakt:
                                                     'araa' || to_char(araa.aanvraagnummer) || <referentietabel> || to_char(<tabel.veld_id>)
                                                     || '@'
                                                     -- Vanaf hier wordt de bestandsnaam gemaakt:
                                                     || stp_adf_taalbundel.get_tekst(p_sleutel => 'STT_ADF_MENU.NAAM:' || araa.amen_id)
                                                     || '-' || <tabel.veld1>
                                                     || '-' || <tabel.veld2>
                                                     || '-' || <tabel.veld3>
                                                     || '-' || <tabel.veld4>
                                                  ,  p_extensie                   => araa.uitvoerformaat
                                               )
            ,  p_aanvraagnummer           => araa.aanvraagnummer
    )   AS araa_splitsen
```

### Splitsquery in DM -> splitsen

![image](https://github.com/fvdsdel/BI_publisher/assets/165891554/f4d71a1a-18ad-494e-b6a8-4370cf81aff6)


```sql
SELECT DISTINCT aras.referentie_id key
     ,  araa.rapport_template template
     ,  araa.taal locale
     ,  araa.uitvoerformaat output_format
     ,  'FILE' del_channel
     ,  oss_adf_config.waarde(null, 'ORACLE-BIP', 'BURSTING-DIRECTORY') parameter1
     ,  aras.bestandsnaam parameter2
FROM stt_adf_rapport_aanvraag araa,
LEFT JOIN stt_adf_rapport_a_splitsen aras ON (araa.aanvraagnummer = aras.aanvraagnummer)
WHERE araa.aanvraagnummer = :p_aanvraagnummer
```

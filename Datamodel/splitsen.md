### Splitsfunctie
'''sql
  , stp_adf_rapport.set_splitsen(p_referentie_id              => <tabel.veld_id> -- ID veld waarop gesplitst/afgeleverd wordt
                                ,  p_referentietabel            => <referentietabel> 
                                ,  p_bestandsnaam               => oss_adf_utility.bestandsnaam(
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
                                ,  p_aanvraagnummer             => araa.aanvraagnummer)                           araa_splitsen
'''

# מקורות ה-PDR – BeeSense

מספור לפי רשימת המקורות ב-`docs/pdr-2027-165.docx` (IEEE, לפי סדר הופעה).

### Background research – precision beekeeping, swarming and hive signals
| # | מקור | קובץ | קישור | איפה מצוטט |
|---|---|---|---|---|
| 1 | Zacepins et al., *Challenges in the development of precision beekeeping*, Biosyst. Eng., 2015 | [[01 - Zacepins 2015 - Precision Beekeeping (abstract page).pdf]] ⚠️ | [DOI](https://doi.org/10.1016/j.biosystemseng.2014.12.001) | 1.1 |
| 2 | Ferrari et al., *Monitoring of swarming sounds…*, Comput. Electron. Agric., 2008 | [[02 - Ferrari 2008 - Swarming sounds (abstract page).pdf]] ⚠️ | [DOI](https://doi.org/10.1016/j.compag.2008.05.010) | 1.1, 2, 3.1, 3.2 – ~110 Hz וטמפרטורה לפני נחילה |
| 3 | Ramsey et al., *The prediction of swarming… vibrational spectra*, Sci. Rep., 2020 | [[03 - Ramsey 2020 - Swarming prediction vibrational spectra.pdf]] | [DOI](https://doi.org/10.1038/s41598-020-66115-5) | 1.1, 2, 3.1 – >90%, עד 30 יום מראש |
| 4 | Meikle & Holst, *Application of continuous monitoring…*, Apidologie, 2015 | [[04 - Meikle Holst 2015 - Continuous monitoring.pdf]] | [DOI](https://doi.org/10.1007/s13592-014-0298-x) | 1.1, 3.1 – משקל רציף, מחזור יומי |

### Existing hive-monitoring systems
| # | מקור | קובץ | קישור | איפה מצוטט |
|---|---|---|---|---|
| 5 | Cecchi et al., *A smart sensor-based measurement system…*, Sensors, 2020 | [[05 - Cecchi 2020 - Smart sensor hive monitoring.pdf]] | [DOI](https://doi.org/10.3390/s20092726) | 2, Table I – RPi, ~4 W, ±10 g |
| 6 | BeeHero, *Technology* | [[06 - BeeHero Technology.pdf]] | [אתר](https://www.beehero.io/technology) | 2, Table I |

### Design data – signal levels, communication and components
| # | מקור | קובץ | קישור | איפה מצוטט |
|---|---|---|---|---|
| 7 | Bencsik et al., *Honeybee colony vibrational measurements to highlight the brood cycle*, PLoS ONE, 2015 | [[07 - Bencsik 2015 - Brood cycle vibrations.pdf]] | [DOI](https://doi.org/10.1371/journal.pone.0141926) | 3.2 – 1–5 µm/s², דופן חלשה פי 10 |
| 8 | Espressif, *ESP-NOW*, ESP-IDF Programming Guide (ESP32-C3) v5.3.2 | [[08 - Espressif ESP-NOW guide.pdf]] | [אתר](https://docs.espressif.com/projects/esp-idf/en/v5.3.2/esp32c3/api-reference/network/esp_now.html) | 3.2 |
| 9 | Avia Semiconductor, *HX711* datasheet | [[09 - HX711 datasheet.pdf]] | [PDF](https://cdn.sparkfun.com/datasheets/Sensors/ForceFlex/hx711_english.pdf) | 3.2 – 50 nV rms |
| 10 | Espressif, *ESP32-C3 series datasheet* | [[10 - ESP32-C3 datasheet.pdf]] | [PDF](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf) | 3.2 – זרמים |

⚠️ [1], [2] הם עמוד התקציר מ-ScienceDirect, לא המאמר המלא (להוריד דרך ספריית בן-גוריון).

### לא מצוטטים כרגע (`not cited/`)
הוסרו מה-PDR כדי לקצר את סקר העבודות הקודמות (25.10.2026):
- Bencsik et al., 2011, *Identification of the honey bee swarming process…* – [DOI](https://doi.org/10.1016/j.compag.2011.01.004) · [גרסה חופשית](https://irep.ntu.ac.uk/id/eprint/14554/)
- BroodMinder-W3 four point weight scale kit – [אתר](https://workerandhive.com/products/broodminder-w3-four-point-weight-scale-kit)

# HydroQC Page

### Installation

- Install [Hydroqc Add-on](https://hydroqc.ca/fr/docs/installation/hass-addon/) 
- Install [Swiss Army Knife Custom Card](https://github.com/amoebelabs/swiss-army-knife-card/).
- Install vertical-stack-in-card from [HACS]
- Install mini-graph-card from [HACS]
- Copy templates in /config/lovelace/sak_templates/templates/layouts/ directory
- Copy theme in /config/themes/ directory
- Add the following sensors in the file sensor.yaml

```
sensor:
  - platform: template
    sensors:
      etat_hydroqc_maison_next_or_current_outage:
        unique_id: "etat_hydroqc_maison_next_or_current_outage"
        friendly_name: "Période de pannes prévues"
        icon_template: mdi:transmission-tower
        value_template: >
          {% if is_state('sensor.hydroqc_maison_next_or_current_outage', 'unavailable') %}
            Aucune 
          {% else %}
            {{ states('sensor.hydroqc_maison_next_or_current_outage') }}
          {% endif %}
        
  - platform: template
    sensors:
      etat_hydroqc_maison_next_pre_heat_start:
        unique_id: "etat_hydroqc_maison_next_pre_heat_start"
        friendly_name: "Prochaine période de pré-chauffage"
        icon_template: mdi:radiator
        value_template: >
          {% if is_state('sensor.hydroqc_maison_next_pre_heat_start', 'unavailable') %}
            Inactif
          {% else %}
            {{ states('sensor.hydroqc_maison_next_pre_heat_start') }}
          {% endif %}
        
  - platform: template
    sensors:
      etat_hydroqc_maison_next_peak_start:
        unique_id: "etat_hydroqc_maison_next_peak_start"
        friendly_name: "Début de la prochaine période de pointe"
        icon_template: mdi:clock-start
        value_template: >
          {% if is_state('sensor.hydroqc_maison_next_peak_start', 'unavailable') %}
            Inactif
          {% else %}
            {{ states('sensor.hydroqc_maison_next_peak_start') }}
          {% endif %}
        
  - platform: template
    sensors:
      etat_hydroqc_maison_next_peak_end:
        unique_id: "etat_hydroqc_maison_next_peak_end"
        friendly_name: "Fin de la prochaine période de pointe"
        icon_template: mdi:clock-end
        value_template: >
          {% if is_state('sensor.hydroqc_maison_next_peak_end', 'unavailable') %}
            Inactif
          {% else %}
            {{ states('sensor.hydroqc_maison_next_peak_end') }}
          {% endif %}
        
  - platform: template
    sensors:
      etat_hydroqc_maison_current_dpc_period_detail:
        unique_id: "etat_hydroqc_maison_current_dpc_period_detail"
        friendly_name: "État du tarif"
        icon_template: mdi:alpha-p-box
        value_template:  >
          {% if is_state('sensor.hydroqc_maison_current_dpc_period_detail', 'normal') %}
            Normal
          {% elif is_state('sensor.hydroqc_maison_current_dpc_period_detail', 'peak') %}
            Pointe
          {% else %}
            {{ states('sensor.hydroqc_maison_current_dpc_period_detail') }}
          {% endif %}     
```

- Restart Home Assistant

### Screenshots

![image](https://user-images.githubusercontent.com/83040228/215606793-b02ae728-a227-4cdf-a5fa-f6370f1aa268.jpeg)

![image](https://user-images.githubusercontent.com/83040228/215606838-c18833b1-3fda-4289-bc9a-0c0ea53d4bcd.jpeg)


### Changelog
#### 1.0
- First release


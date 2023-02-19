# HqCombo Page

### Installation

- Install [Hydroqc Add-on](https://hydroqc.ca/fr/docs/installation/hass-addon/) 
- Install [Swiss Army Knife Custom Card](https://github.com/amoebelabs/swiss-army-knife-card/).
- Install vertical-stack-in-card from [HACS]
- Install Apexcharts-card from [HACS] 
- Copy the folowing templates in /config/lovelace/sak_templates/templates/layouts/ directory
  - sak-layout-mjt-kwh-total-regulier-pointe.yaml
  - sak-layout-mjt-moyennes.yaml
  - sak-layout-mjt-periode-actuelle.yaml
  - sak_layout_mjt_production_demande.yaml
- Copy theme in /config/themes/ directory
- Copy the HqCombo.yaml

- Add the following sensors in the file sensor.yaml

```
# États des période Hydro-Québec
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
            {% set heure = as_timestamp(states('sensor.hydroqc_maison_next_or_current_outage')) | timestamp_custom('%H:%M') %}
            {% set journee = ["Lun", "Mar","Mer","Jeu","Ven","Sam","Dim"] %}
            {{ journee[as_timestamp(states('sensor.hydroqc_maison_next_or_current_outage')) | timestamp_custom('%w' ) | int -1 ] }} {{ heure }}
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
            {% set heure = as_timestamp(states('sensor.hydroqc_maison_next_pre_heat_start')) | timestamp_custom('%H:%M') %}
            {% set journee = ["Lun", "Mar","Mer","Jeu","Ven","Sam","Dim"] %}
            {{ journee[as_timestamp(states('sensor.hydroqc_maison_next_pre_heat_start')) | timestamp_custom('%w' ) | int -1 ] }} {{ heure }}
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
            {% set heure = as_timestamp(states('sensor.hydroqc_maison_next_peak_start')) | timestamp_custom('%H:%M') %}
            {% set journee = ["Lun", "Mar","Mer","Jeu","Ven","Sam","Dim"] %}
            {{ journee[as_timestamp(states('sensor.hydroqc_maison_next_peak_start')) | timestamp_custom('%w' ) | int -1 ] }} {{ heure }}
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
            {% set heure = as_timestamp(states('sensor.hydroqc_maison_next_peak_end')) | timestamp_custom('%H:%M') %}
          {% set journee = ["Lun", "Mar","Mer","Jeu","Ven","Sam","Dim"] %}
            {{ journee[as_timestamp(states('sensor.hydroqc_maison_next_peak_end')) | timestamp_custom('%w' ) | int -1 ] }} {{ heure }}
          {% endif %}
        
  - platform: template
    sensors:
      etat_hydroqc_maison_current_dpc_period_detail:
        unique_id: "etat_hydroqc_maison_current_dpc_period_detail"
        friendly_name: "État du tarif"
        icon_template: mdi:currency-usd
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

## Screenshots

![image](https://user-images.githubusercontent.com/83040228/218573003-8443f281-ee8d-4a0b-b79b-3a6fdbb2691c.jpeg)

![image](https://user-images.githubusercontent.com/83040228/218573046-0415498c-cccb-4e31-b05f-f0d3e3b407b2.jpeg)

### Changelog
#### 1.0
- First release

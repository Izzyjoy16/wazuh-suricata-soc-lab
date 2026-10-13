# Detection Finding: Suricata DNS Alert in Wazuh

## Summary

A controlled lab test demonstrated that Wazuh can collect a Suricata JSON event, decode its fields, match a Suricata detection rule, and record the resulting alert.

## Detection Details

- **Suricata signature:** `LAB DNS query for www.example.com`
- **Wazuh rule ID:** `86601`
- **Wazuh alert description:** `Suricata: Alert - LAB DNS query for www.example.com`
- **Wazuh alert level:** 3
- **Event source:** `/tmp/suricata-wazuh-test.json`
- **Sample source IP:** `192.168.170.8`
- **Sample destination IP:** `192.168.170.20`
- **Protocol:** UDP
- **Destination port:** 53 (DNS)

## Validation Steps

1. Analyzed a sample DNS PCAP with Suricata.
2. Generated a custom Suricata DNS detection event.
3. Configured Wazuh to monitor Suricata JSON events.
4. Used `wazuh-logtest` to confirm JSON decoding and rule matching.
5. Appended a copy of the sample alert to the temporary test file.
6. Verified the resulting Wazuh alert in `alerts.json`.

## Result

**Pass:** Wazuh recorded the test event with rule ID `86601` and the expected Suricata alert description.

## Limitations

The packet capture is historical sample data dated 2005. The final end-to-end test used a copied event in a temporary file, not a newly observed live network attack. This test validates the event ingestion and rule-matching pipeline; it does not demonstrate live network monitoring, automatic blocking, or a real-time threat.

## Remediation / Next Steps

- Capture and document the successful Wazuh alert.
- Verify the Wazuh dashboard and indexer separately.
- For ongoing monitoring, configure Suricata to produce live EVE JSON events and validate that those events reach Wazuh.

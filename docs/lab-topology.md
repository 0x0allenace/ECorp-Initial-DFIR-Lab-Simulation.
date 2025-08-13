# My Lab Topology

Here’s the network diagram for the ECorp DFIR setup:

![Lab Topology Diagram](/images/labtopography.png)

The diagram above shows the PfSense acting as router and firewall to the AttackLAN and ECorp subnets.

## Notes
- Each VM has a static IP set in PfSense.
- Velociraptor agents report to the central GUI on port 8000.

# Partner Power Hour - TShooting With the OSI Model

Speaker: Matt Raio

IT Operations, more or less, since 1997.

Worked at startup GNS3 (virtual networking software).

## Summary Notes and Key Takeaways

OSI Model is conceptual.

7-layer model where each layer adds header information, so facilite communications.

Application - End user, software
Presentation - Encryption, decryption, and data arrangement
Session - Synchronization and Port addressing
Transport - TCP and other un/connected nodes
Network - Primary addressing layer
Data Link - Hardware addressing layer
Physical - Actual interfaces link network cards

Top-down troubleshooting approach:

- Start with application information including error messages

Bottom-up troubleshooting approach:

- Check the physical hardware, power, and physical connections
- Then look at switching and routing equipment

Divide and Conquer

- Pick-and-choose a layer that *might* be source of the problem

How well can you articulate the problem?

- Talking through the issue will help you to see the gaps in understanding of the problem

Try to select a tactic to resolve the problem.

- top-to-bottom
- bottom-to-top

Implement tests

- Will help find boundaries of the problem
- Will help confirm when the problem has the resolved

Review results

- A desired result might not be the full solution
- False Negative: Results come back, but not as anticipated

Tools for Troubleshooting

- Utilize tools that are proper for the environment the problem is in
- WiFi network? Access a wifi router or WAP logs for hints

## Footer

Return to [root readme](../README.html)

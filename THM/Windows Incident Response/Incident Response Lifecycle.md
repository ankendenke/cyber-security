## What Is Incident Response

Incident Response (IR) refers to the processes and technologies an organization employs to detect and react to cyber threats, security breaches, or cyber attacks. Implementing a formal incident response plan empowers cyber security teams to mitigate or prevent damage effectively.

Ideally, an organization establishes incident response procedures and technologies within a formal incident response plan, detailing the specific steps for identifying, containing, and resolving various types of cyber attacks.

Organizations that need to define their incident response processes in a complete and effective manner can refer to two of the most commonly used frameworks, released respectively by the NIST (National Institute of Standards and Technology) and by SANS (Sysadmin, Audit, Network, and Security), a private organization that focuses on researching cyber security topics.

![Four arrows in a circle connecting four boxes. The arrows go from 'Preparation', to 'Detection and Analysis', to 'Containment, Eradication, and Recovery', to 'Post-Incident Activity', and back to 'Preparation'.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1730828994819.png)

The **NIST Incident Response Framework** involves 4 steps:

1. **Preparation**: Establishing and maintaining an incident response capability.
2. **Detection and Analysis**: Identifying and understanding the scope and impact of an incident.
3. **Containment, Eradication, and Recovery**: Limiting the incident's impact, eliminating the threat, and restoring normal operations.
4. **Post-Incident Activity**: Reviewing and improving the incident response process and documentation.

This framework falls into the context of the NIST Cybersecurity Framework, which is a much broader set of guidelines for mitigating organizational cyber security risks at all levels.

**SANS Incident Response 101**, on the other hand, splits out the containment, eradication, and recovery into different steps, making the whole process comprised of 6 steps: preparation, identification, containment, eradication, recovery, and lessons learned.

Both frameworks can and are currently used by organizations worldwide to aid with the development of an effective Incident Response Plan.

## Incident Response Is a Process

_“Security is not a product, but a process” - Bruce Schneier_

This quote by the famous American cryptographer, computer security professional, privacy specialist, and writer Bruce Schneier can be applied to anything cyber security, from incident handling and response to threat intelligence, vulnerability management, threat hunting, etc.

Stating that security is a process is a very concise way to convey the idea that security cannot be achieved simply by purchasing and deploying security products or tools. Instead, true security requires ongoing, comprehensive efforts that comprise a wide range of activities and practices. Security is a dynamic, multifaceted process that requires a coordinated and continuous effort. It's about creating a resilient system that must adapt to new challenges and threats over time.

Keeping this concept in mind, we can look at the NIST Incident Response Framework steps not as a mere “to-do” list that we can archive once we've completed all phases. Rather, we should view it as a continuous lifecycle, with each step feeding new information to the next and each new incident providing valuable insights into the organization's security stance. These insights can be learned during the post-incident activity (or lessons learned) step and must feed a new incident response cycle with improvements to be integrated during the next preparation phase.

## The Incident Responder Mindset

As incident responders, we are usually called to action in the middle of the second phase of the NIST Incident Response Framework: right after our detection tools or policies have fired an alert, prompting a deep analysis of the anomalies.

Getting thrown into the process in the middle of an emergency, with panic and urgency pushing us to find a solution ASAP (yes, it's yelled), we might lose sight of the big picture and forget one of the main goals of an incident response cycle: to feed new information to the next cycle. Thus, it's crucial that we document every step we take and every new information we gather. As incident responders, we must always remember that we have a double goal: to eradicate the threat and prevent it from impacting our organization a second time.

With these two goals in mind, let's delve into our scenario and start our analysis.
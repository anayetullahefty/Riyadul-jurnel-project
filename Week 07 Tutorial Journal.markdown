## Task 2

**AP Information**:
1. **AP 1**:
   - **SSID**: he!!o
   - **BSSID**: 58:11:22:14:43:0c
   - **Frequency Band**: 2.4 GHz
   - **Channel**: 6
   - **Data Rate**: 30 Mbps
2. **AP 2**:
   - **SSID**: Virous!
   - **BSSID**: 62:83:e7:22:ea:93
   - **Frequency Band**: 5 GHz
   - **Channel**: 5
   - **Data Rate**: 100 Mbps

## Task 3

**Important Settings and Considerations**:

1. **SSID**: 
   - **Current**: "he!!o"
   - **Consideration**: Change to a unique name like "SmithHome5G" to distinguish from neighbors’ networks and indicate 5 GHz band for clarity, especially in a dense apartment complex.
   - **Reason**: Reduces confusion for devices and users, improving connection reliability.
2. **Channel**: 
   - **Current**: Auto (2.4 GHz, Channel 6; 5 GHz, Channel 36)
   - **Consideration**: For 2.4 GHz, manually set to Channel 1, 6, or 11 based on WiFi Analyzer’s interference data (e.g., Channel 1 if least congested). For 5 GHz, set to a high channel (e.g., 149) to avoid radar interference.
   - **Reason**: Manual channel selection minimizes overlap with nearby APs, boosting performance in crowded areas.

3. **Security Mode**: 
   - **Current**: WPA2-PSK
   - **Consideration**: Upgrade to WPA3 if all devices support it (check compatibility for older devices like IoT gadgets).
   - **Reason**: WPA3 offers stronger encryption and protection against brute-force attacks, critical for securing sensitive data like university assignments.

4. **QoS (Quality of Service)**: 
   - **Current**: Disabled
   - **Consideration**: Enable QoS to prioritize bandwidth for critical applications like Zoom for online classes or Blackboard access, limiting bandwidth for non-essential tasks like streaming.
   - **Reason**: Ensures stable performance for academic tasks in a shared household with multiple users.

5. **Access Control**: 
   - **Current**: Disabled
   - **Consideration**: Enable Access Control to whitelist only known devices (e.g., by MAC address, such as my laptop and phone) and block unauthorized devices.
   - **Reason**: Prevents unauthorized access, critical in a university context where roommates or visitors might attempt to connect, potentially compromising network security.

6. **Parental Controls**: 
   - **Current**: Disabled
   - **Consideration**: Enable Parental Controls to restrict access for specific devices (e.g., a sibling’s tablet) during study hours (e.g., 8 AM–6 PM) or block inappropriate content.
   - **Reason**: Maintains a distraction-free environment for studying, especially during exam periods, by limiting non-academic internet use.

**Screenshot**: The screenshot from my TP-Link Archer BE400  emulator shows the Wireless Settings page, displaying SSID ("TP-Link_5G"), Security (WPA2-PSK) etc.

## Task 4: Self-Evaluation of Teamwork

**Generative AI Prompt and Output**:

- **Prompt**: "List 5 ways to improve teamwork in a university group project."
- **Output**:
  1. Establish clear communication channels.
  2. Define roles and responsibilities early.
  3. Schedule regular team meetings.
  4. Use collaborative tools for task management.
  5. Foster a respectful and inclusive environment.

- **Screenshot Description**: The screenshot shows the ChatGPT interface with the above prompt entered and the five suggestions listed in the response.

**Comparison with Team Practices**:

1. **Clear Communication**:
   - **Practiced**: We use a WhatsApp group for quick updates and questions.
   - **Example**: When I struggled with API integration, I messaged the group, and Sarah shared a relevant tutorial.
2. **Defined Roles**:
   - **Practiced**: Roles were assigned in Week 3 (e.g., I’m coding the backend, John handles frontend).
   - **Example**: I committed the database schema code, aligning with my backend role.
3. **Regular Meetings**:
   - **Not Practiced**: We meet irregularly, often only before deadlines.
   - **Improvement**: Schedule weekly 30-minute Zoom meetings to review progress and plan tasks.
4. **Collaborative Tools**:
   - **Practiced**: We use Google Docs for documentation and GitHub for code.
   - **Example**: Our project report draft is in a shared Google Doc, edited by all members.
5. **Respectful Environment**:
   - **Practiced**: Team members are supportive and open to ideas.
   - **Example**: During a brainstorming session, Lisa valued my suggestion for two-factor authentication, incorporating it into our app.

**GitHub Commit Analysis**:

- **Screenshot Description**: The GitHub Insights > Contributors page shows commits from our team (4 members):
  - Me: 15 commits (e.g., backend API, database setup).
  - John: 12 commits (e.g., UI components).
  - Sarah: 8 commits (e.g., security features).
  - Lisa: 6 commits (e.g., documentation, testing).
- **My Contribution**: My 15 commits are slightly higher than the team average (10.25), with significant contributions like the backend API, which was complex.
- **Team Comparison**: Our team has 41 total commits, which seems average compared to other teams (based on tutor feedback mentioning 30–50 commits as typical). Contribution

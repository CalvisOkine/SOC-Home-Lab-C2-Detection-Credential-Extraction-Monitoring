# SOC Home Lab: C2 Detection & Credential Extraction Monitoring

---

### **Introduction**

This lab draws its inspiration from Eric Capuano’s original blog post which is not now unavailable, but you can still follow the concepts by watching Gerald Auger’s detailed video walkthrough on his YouTube channel. The link to the video will be referenced below. This lab simulates a blue team exercise focused on detecting Command & Control (C2) activity and monitoring suspicious process behavior (e.g., LSASS memory dumping). The objectives include:

- Deploying a C2 framework (Sliver) to emulate adversary tactics.
- Configuring LimaCharlie for real-time detection of credential extraction attempts.
- Analyzing alerts and refining detection rules.

---

### **Lab Setup**

**Virtual Machines**

- **Attacker VM (Ubuntu):** `10.0.2.3`
    - Tools: Sliver C2 server.
- **Target VM (Windows):** `10.0.2.5`
    - Tools: LimaCharlie agent, simulated user activity.

**Network Configuration**

- Both VMs are on the same subnet (`10.0.2.0/24`) with bidirectional communication.

---

### **C2 Infrastructure with Sliver**

1. **Start the Sliver Server**
    
     ![image](https://github.com/user-attachments/assets/81fa3ade-3d83-472c-a45e-3695d2c0e39f)


    

2. **Generate and Deploy Implant**
    
     ![image 1](https://github.com/user-attachments/assets/7c3fe823-ed8d-4320-87a5-810398e128ad)

    

3. **Start HTTP Listener**

     ![image 2](https://github.com/user-attachments/assets/c416cdde-7b59-4174-8882-5eb916732765)





---

### **Monitoring with LimaCharlie**

1. **Deploy LimaCharlie Agent**
    - Install the agent on the Windows VM and link it to your LimaCharlie dashboard.
2. **Create Detection Rule**
    - Rule logic: Trigger an alert if `lsass.exe` is accessed or dumped.
        
        ![image 3](https://github.com/user-attachments/assets/4c9124ff-dcb0-4df9-b1b7-e3b846671b6a)
        

---

### **Executing the Attack**

1. **Run the Implant**
    - Execute the Sliver payload on the Windows VM from the C2 server.
        
        ![image 4](https://github.com/user-attachments/assets/e7b3a437-5412-4b6a-a243-8a0f88cb0531)

        
2. **Dump LSASS Memory**
    
    ![image 5](https://github.com/user-attachments/assets/fb026d71-328a-4502-b869-bc4570c110cf)

    
    - LimaCharlie generates an alert:
        
   ![image 6](https://github.com/user-attachments/assets/b46047d0-9aae-4d76-b8a7-effa9409f3fb)

        

---

### **Analysis & Reporting**

1. **Review Alerts**
    - Investigate the LimaCharlie dashboard for process details (command line, memory usage, hash).
        
        ![image 7](https://github.com/user-attachments/assets/3de3326f-c3a1-42c9-a1b8-a7a80713ad8f)

        

---

### **Conclusion**

We saw how an attacker might use a tool like Sliver to gain control of a machine and why it’s so important to monitor critical system processes. By setting up detection rules in SIEM tools like LimaCharlie, we learned how to catch suspicious activities early. The exercise emphasizes that cybersecurity isn’t just about preventing attacks, it’s also about being ready to detect and respond to them quickly.

### Reference:

Gerald Auger Walkthrough Video: [https://youtu.be/oOzihldLz7U](https://youtu.be/oOzihldLz7U)

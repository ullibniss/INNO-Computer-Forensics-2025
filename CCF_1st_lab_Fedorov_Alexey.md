# CCF Lab 1: Data Acquisition

## Complete by Fedorov Alexey (tg @ullibniss)

---

## Task 1 - Setting up your environment

```
You need to prepare 2 USB drive
```

Unfortunately, I don't have USB drives. Because of this I will use CAINE ISO image for live environment in VMbox and emulate drive for `drive A` with `loop` device.

## 1.1 The first one should have a CAINE live environment that will be used to collect evidence.

I downloaded `CAINE 14.0 "LIGHTSTREAM"`. The file called `caine14.0.iso`. I installed it on VMbox.


## 1.2 On the second one (this drive will be called drive A) you should deploy that disk image. The disk image is compressed with special utility that preserves original bits intact. You should uncompress it (using FTK imager) and burn it on the ash drive (do not forget about unallocated space).

I am not used `FTK image`, because my host operation system is `Ubuntu`. I used `xmount` to mount E01 image.

```
xmount --in ewf --out raw /home/ullibniss/Downloads/evidence1.E01 /mnt/usb1
```

And I got the following files.

![image](https://github.com/user-attachments/assets/7d00ed3b-42e3-407c-a86f-5f51b3416f1f)

Then I got start sector and type of filesystem on `.dd` image with `cfdisk`

![image](https://github.com/user-attachments/assets/050964be-81ad-4e35-b103-8e9d22e8fdf5)

Next step I create `loop` device for `evidence.dd`.

![image](https://github.com/user-attachments/assets/cc469aa1-fd71-47cd-8fa0-0041a7b109d6)

Final step, I mounted this `loop` device to `usb2`.

![image](https://github.com/user-attachments/assets/db926c66-71a3-4758-bcfe-b56f29c3df4a)

# Task 2 - Imaging

## 2.1 Discuss how you can retrieve an image from an, currently off-line, USB stick in a forensically sound manner. Create and describe this method.

Retrieving an image from an offline USB stick in a forensically sound manner requires adhering to digital forensic best practices to ensure data integrity, chain of custody, and legal admissibility. 



## 2.2 Write a one-line description, or note a useful feature for the following tools included in CAINE: Guymager, Disk Image Mounter, dcdd / dc3dd, kpartx.

Here are one-line descriptions of each tool:

- `Guymager` - forensic imaging tool with support for multiple formats (DD/EWF/AFF) and hash verification.

- `Disk Image Mounter` - quickly mounts forensic images in read-only mode for analysis.

- `dc3dd/dcdd` - Enhanced version of dd with progress display and error handling for forensics.

- `kpartx` - Creates device mappings for partitions within disk images.

## 2.3 . Follow your method to retrieve the image from drive A. Please use timestamps, explain every tool and note down the version. For the purpose of speed. Make sure both team members have access to the retrieved image. You can use your PCs as an evidence sharing platform.

I will retrieve the image from drive A using `dc3dd` tool. First I need to mount forward directory to `CAINE` virtual machine. 

## 2.4 

### 2.4.1 Why Use a Forensic Distribution? Main Differences vs. Regular Linux Distros  

A `CAINE` is specifically designed for **digital forensics and incident response**, whereas a **regular Linux distribution** (e.g., Ubuntu, Fedora) is a general-purpose OS.  

#### **Key Differences:**  

| **Feature**               | **Forensic Distribution (CAINE)** | **Regular Linux Distribution** |
|---------------------------|----------------------------------|--------------------------------|
| **Default Write Protection** | Automatically blocks writes to evidence drives | May auto-mount and modify storage |
| **Pre-installed Forensic Tools** | Includes tools like Autopsy, Guymager, dd, The Sleuth Kit | Requires manual installation |
| **Live Environment Focus** | Optimized for bootable USB/CD forensic analysis | Primarily meant for installation |
| **Legal & Forensic Policies** | Follows forensic best practices (e.g., hashing, chain of custody) | No built-in forensic compliance |
| **Minimal Background Processes** | Reduces interference with evidence | May run unnecessary services |

### 2.4.2 When to Use a Live Environment vs. Installed Environment?  

| **Scenario** | **Live Environment (USB/CD)** | **Installed Environment (HDD/VM)** |
|-------------|-----------------------------|----------------------------------|
| **Field Investigations** | Portable, no installation needed | Requires setup |
| **Evidence Acquisition** | Safe, read-only by default | Risk of modification |
| **Long-Term Analysis** | Slower, no persistence | Faster, saves progress |
| **Malware Analysis** | Isolated, no HDD risk | Risk of infection |
| **Training & Labs** | No saved changes | Persistent storage |

### 2.4.3 CAINE Linux Policies  

CAINE follows strict forensic policies to ensure **integrity, reproducibility, and legal compliance**:  
 
1. **Read-Only by Default**  
   - Automatically enables **write-blocking** for attached storage.  
   - Prevents accidental modification of evidence.  

2. **Forensic Toolset Integration**  
   - Includes **Autopsy, Guymager, Wireshark, Volatility, RegRipper**, etc.  
   - Ensures investigators have all necessary tools without manual setup.  

3. **Chain of Custody & Documentation**  
   - Encourages **logging** (timestamps, hashes, examiner notes).  
   - Supports **report generation** for legal proceedings.  

4. **Non-Intrusive Operation**  
   - Minimizes background processes to avoid altering evidence.  
   - Disables **auto-mounting** and **swap memory** to prevent data leaks.  

5. **Open Source & Reproducibility**  
   - All tools are **FOSS (Free & Open Source)** for transparency.  
   - Ensures methods can be **independently verified**.  

6. **Privacy & Ethical Use**  
   - Designed **only for lawful investigations** (not for hacking).  
   - Follows **international forensic standards**.
  
## 2.5 As soon as your dump nishes, start a tool to create a timeline on the image. You will need this timeline later in the assignment. Hints: log2timeline.py.

I got a timeline from dumped image.

![image](https://github.com/user-attachments/assets/800762f0-c70b-46c9-93fe-3c8f5af32991)

I also can analyze it with `Plaso` tools.

![image](https://github.com/user-attachments/assets/0d90f699-f0ef-4b51-add2-67168574271d)

## Task 3 - Verfication

```
Verication of the retrieved evidence is also required. You are going to exchange your evidence
between your group of students. This can be done by sharing your USB device (drive A) with your
teammate.
```


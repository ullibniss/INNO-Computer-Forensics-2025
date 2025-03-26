![image](https://github.com/user-attachments/assets/0f354843-66ab-40df-92b7-44470d3fdf95)# CCF Lab 1: Data Acquisition

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

##

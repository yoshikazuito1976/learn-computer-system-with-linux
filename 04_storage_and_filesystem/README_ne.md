# 04 Storage र Filesystem

## यस अध्यायको विषय

कम्प्युटर CPU र memory मात्रले निरन्तर काम गर्न सक्दैन।

तपाईंले बनाएका file, install गरेका software, configuration file, log आदि data बिजुली बन्द गरेपछि पनि बाँकी रहने ठाउँमा सुरक्षित हुन्छन्।

यस अध्यायमा हामी Linux मा निम्न कुराहरू अवलोकन गर्नेछौँ।

- Storage भनेको के हो
- Filesystem भनेको के हो
- Directory structure भनेको के हो
- Mount गर्नु भनेको के हो
- Disk capacity र usage कसरी जाँच गर्ने
- inode भनेको के हो

---

## 1. Storage भनेको के हो?

Storage भनेको data सुरक्षित गर्न प्रयोग हुने device हो।

Storage का सामान्य उदाहरणहरू:

- HDD
- SSD
- USB memory
- SD card
- Virtual disk

Linux मा यी device हरूलाई पनि file जस्तै व्यवहार गरिन्छ।

---

## 2. Storage Device जाँच गर्ने

पहिले Linux ले चिनेका storage device हरू जाँच गरौँ।

```bash
lsblk
```

`lsblk` `block device` हरूको सूची देखाउने command हो।

`block device` भनेको data लाई निश्चित आकारका block मा पढ्ने र लेख्ने device हो।

उदाहरण:

```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   64G  0 disk
├─sda1   8:1    0    1G  0 part /boot
└─sda2   8:2    0   63G  0 part /
```

यस उदाहरणबाट निम्न कुरा बुझ्न सकिन्छ।

- `sda` पूरा disk हो
- `sda1` र `sda2` partition हुन्
- `/` र `/boot` mount point हुन्

---

## 3. Partition भनेको के हो?

Partition भनेको एउटा storage device लाई विभाजन गरिएको क्षेत्र हो।

उदाहरणका लागि, एउटा SSD लाई यसरी विभाजन गर्न सकिन्छ।

- OS राख्ने क्षेत्र
- Boot का लागि क्षेत्र
- Data राख्ने क्षेत्र

Linux मा प्रत्येक partition मा filesystem बनाएर प्रयोग गरिन्छ।

जाँच गरौँ।

```bash
sudo fdisk -l
```

वा filesystem को प्रकार पनि हेर्न निम्न command प्रयोग गर्न सकिन्छ।

```bash
lsblk -f
```

---

## 4. LVM (Logical Volume Manager) भनेको के हो?

LVM भनेको physical disk वा partition लाई अझ लचिलो तरिकाले व्यवस्थापन गर्ने प्रणाली हो।

सामान्य partition मा एक पटक बनाएपछि size परिवर्तन गर्न गाह्रो हुन सक्छ।

LVM प्रयोग गर्दा निम्न कामहरू सजिलै गर्न सकिन्छ:

- धेरै disk लाई एउटै volume मा जोड्ने
- logical volume को size पछि बढाउने वा घटाउने
- maintenance कामका लागि snapshot बनाउने

LVM लाई प्रायः यी 3 तहमा बुझिन्छ:

- PV (Physical Volume): physical disk वा partition
- VG (Volume Group): PV हरूलाई समूह बनाएको भाग
- LV (Logical Volume): filesystem बनाउने logical क्षेत्र

सम्बन्ध यस्तो हुन्छ:

```text
Physical disk/partition (PV) -> Volume group (VG) -> Logical volume (LV)
```

LVM को स्थिति जाँच गर्न प्रायः यी command प्रयोग गरिन्छ:

```bash
sudo pvs
sudo vgs
sudo lvs
```

LVM प्रयोग भएको अवस्थामा `lsblk` को `TYPE` स्तम्भमा `lvm` देखिन सक्छ।

---

## 5. Filesystem भनेको के हो?

Filesystem भनेको storage मा file र directory सुरक्षित तथा व्यवस्थापन गर्ने प्रणाली हो।

प्रमुख filesystem का उदाहरणहरू:

| Filesystem | मुख्य प्रयोग |
| --- | --- |
| ext4 | Linux मा धेरै प्रयोग हुने |
| xfs | RHEL आधारित system, जस्तै AlmaLinux मा धेरै प्रयोग हुने |
| btrfs | snapshot जस्ता advanced feature भएको |
| vfat | USB memory मा कहिलेकाहीँ प्रयोग हुने |
| ntfs | Windows मा धेरै प्रयोग हुने |

हालको environment मा प्रयोग भइरहेको filesystem जाँच गरौँ।

```bash
df -T
```

---

## 6. Mount भनेको के हो?

Mount भनेको storage device वा partition लाई Linux को directory structure भित्र जोड्नु हो।

Linux ले Windows जस्तै `C:` वा `D:` जस्ता drive name प्रयोग गरेर storage व्यवस्थापन गर्दैन।

Linux मा सबै file र directory `/` बाट सुरु हुने एउटै tree structure भित्र राखिन्छन्।

उदाहरण:

```text
/
├── boot
├── home
├── var
├── etc
└── tmp
```

Storage device फरक भए पनि त्यो कुनै directory मा जोडिन्छ।

Mount स्थिति जाँच गरौँ।

```bash
mount
```

जानकारी धेरै भएमा `grep` सँग मिलाएर प्रयोग गर्न सकिन्छ।

```bash
mount | grep "^/dev"
```

वा अझ सजिलोसँग हेर्न निम्न command प्रयोग गर्न सकिन्छ।

```bash
findmnt
```

---

## 7. Disk Capacity जाँच गर्ने

Disk usage जाँच गर्न `df` command प्रयोग गरिन्छ।

```bash
df -h
```

`-h` को अर्थ human readable हो।

यसले मानिसले सजिलै पढ्न सक्ने unit मा size देखाउँछ।

उदाहरण:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        63G   12G   51G  20% /
```

यसबाट निम्न कुरा बुझ्न सकिन्छ।

- कुल क्षमता: 63G
- प्रयोग भएको: 12G
- खाली: 51G
- प्रयोग प्रतिशत: 20%
- Mount point: /

---

## 8. Directory अनुसार Usage जाँच गर्ने

`df` filesystem को पूरा usage जाँच गर्ने command हो।

Directory अनुसार capacity जाँच गर्न `du` प्रयोग गरिन्छ।

```bash
du -sh /var
```

अर्थ:

- `du`: disk usage
- `-s`: summary
- `-h`: human readable

धेरै directory तुलना गर्न पनि सकिन्छ।

```bash
sudo du -sh /var/* 2>/dev/null
```

`/var` मा log, cache जस्ता बारम्बार परिवर्तन हुने data राखिन्छ।

---

## 9. inode भनेको के हो?

Linux filesystem मा file name भन्दा अलग, वास्तविक file व्यवस्थापन गर्ने जानकारी हुन्छ।

यस व्यवस्थापन जानकारीलाई inode भनिन्छ।

inode मा यस्ता जानकारीहरू हुन्छन्।

- Owner
- Permission
- File size
- Update time
- Data को स्थान

inode number जाँच गरौँ।

```bash
ls -i
```

उदाहरण:

```text
123456 README.md
```

`123456` जस्तो number inode number हो।

---

## 10. File Name र inode को सम्बन्ध

File name मानिसले सजिलै प्रयोग गर्न सक्ने नाम हो।

तर Linux filesystem भित्र file हरू inode प्रयोग गरेर व्यवस्थापन गरिन्छ।

अर्थात् file name inode लाई देखाउने label जस्तै हो।

जाँच गरौँ।

```bash
touch sample.txt
ls -li sample.txt
```

अब hard link बनाऔँ।

```bash
ln sample.txt sample_link.txt
ls -li sample.txt sample_link.txt
```

दुई file name ले एउटै inode number देखाइरहेको कुरा पुष्टि गर्न सकिन्छ।

---

## 11. Symbolic Link सँगको फरक

Symbolic link अर्को file तर्फको reference हो।

```bash
ln -s sample.txt sample_symlink.txt
ls -li sample.txt sample_symlink.txt
```

Symbolic link को inode original file भन्दा फरक हुन्छ।

जाँच गरौँ।

```bash
ls -l sample_symlink.txt
```

उदाहरण:

```text
sample_symlink.txt -> sample.txt
```

---

## 12. /etc/fstab भनेको के हो?

`/etc/fstab` startup को समयमा कुन filesystem कहाँ mount गर्ने भनेर निर्धारण गर्ने file हो।

यसको सामग्री जाँच गरौँ।

```bash
cat /etc/fstab
```

वा:

```bash
less /etc/fstab
```

`/etc/fstab` महत्वपूर्ण configuration file हो।

गलत तरिकाले edit गरिएमा OS सही रूपमा boot नहुन सक्छ।

यस अध्यायमा edit नगरी, केवल जाँच मात्र गरिन्छ।

---

## 13. अभ्यास: Filesystem अवलोकन गर्ने

निम्न कुराहरू जाँच गरी परिणाम `04_storage_report.txt` मा सुरक्षित गरौँ।

### 1. हालको directory जाँच गर्ने

```bash
pwd >> 04_storage_report.txt
```

### 2. Block device जाँच गर्ने

```bash
lsblk >> 04_storage_report.txt
```

### 3. Filesystem type जाँच गर्ने

```bash
df -T >> 04_storage_report.txt
```

### 4. Disk capacity जाँच गर्ने

```bash
df -h >> 04_storage_report.txt
```

### 5. Mount स्थिति जाँच गर्ने

```bash
findmnt >> 04_storage_report.txt
```

### 6. /var को size जाँच गर्ने

```bash
sudo du -sh /var 2>/dev/null >> 04_storage_report.txt
```

### 7. inode number जाँच गर्ने

```bash
ls -li >> 04_storage_report.txt
```

### 8. LVM जानकारी जाँच गर्ने

```bash
{
	echo "== pvs =="
	sudo pvs 2>/dev/null || echo "LVM को PV भेटिएन"
	echo "== vgs =="
	sudo vgs 2>/dev/null || echo "LVM को VG भेटिएन"
	echo "== lvs =="
	sudo lvs 2>/dev/null || echo "LVM को LV भेटिएन"
} >> 04_storage_report.txt
```

---

## 14. विचार प्रश्नहरू

निम्न प्रश्नहरूको उत्तर आफ्नै शब्दमा लेख्नुहोस्।

### Q1. Storage र memory मा के फरक छ?

Hint:

- बिजुली बन्द भएपछि data बाँकी रहन्छ कि रहँदैन
- CPU ले प्रत्यक्ष रूपमा काम गर्न प्रयोग गर्छ कि गर्दैन
- File सुरक्षित गर्ने ठाउँ हो कि होइन

---

### Q2. Filesystem केका लागि प्रयोग हुन्छ?

Hint:

- File name
- Directory
- Owner
- Permission
- Storage location

---

### Q3. Linux मा `C:` वा `D:` प्रयोग नगरी किन `/` बाट सुरु हुने structure प्रयोग गरिन्छ?

Hint:

- सबै कुरा एउटै directory structure भित्र व्यवस्थापन हुन्छ
- अर्को storage पनि कुनै directory मा जोडिन्छ
- Mount को विचार

---

### Q4. `df` र `du` मा के फरक छ?

Hint:

- पूरा filesystem हेर्ने
- Directory वा file अनुसार हेर्ने

---

### Q5. inode भनेको के हो?

Hint:

- File name आफैँ होइन
- File को व्यवस्थापन जानकारी
- Hard link सँग सम्बन्धित

---

## 15. यस अध्यायको सारांश

यस अध्यायमा तपाईंले Linux मा storage र filesystem बारे सिक्नुभयो।

मुख्य बुँदाहरू:

- Storage data सुरक्षित गर्ने device हो
- Partition storage लाई विभाजन गरिएको क्षेत्र हो
- LVM storage लाई समूहमा बाँधेर लचिलो रूपमा व्यवस्थापन गर्ने प्रणाली हो
- Filesystem file र directory व्यवस्थापन गर्ने प्रणाली हो
- Linux मा सबै file `/` बाट सुरु हुने tree structure भित्र राखिन्छन्
- Mount ले storage लाई directory structure मा जोड्छ
- `df` ले पूरा filesystem को capacity जाँच गर्न सक्छ
- `du` ले directory अनुसार usage जाँच गर्न सक्छ
- inode file को व्यवस्थापन जानकारी हो

Storage र filesystem, log management, user management, permission management, र security सँग गहिरो सम्बन्ध राख्छन्।

यो अध्याय आगामी Linux अध्ययनको आधार हो।

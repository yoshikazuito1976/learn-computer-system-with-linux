# 01_os_and_distribution

## यस अध्यायको उद्देश्य

यस अध्यायमा तपाईं Linux वातावरणमा **OS**, **Linux kernel**, र **distribution** बीचको फरक बुझ्नुहुनेछ।

कम्प्युटर प्रणालीको अध्ययनमा "OS" भन्ने शब्द धेरै पटक आउँछ।
तर Linux प्रयोग गर्दा तलका शब्दहरू छुट्ट्याएर बुझ्न आवश्यक हुन्छ।

* OS
* Linux
* Linux kernel
* Distribution
* Version
* Architecture

यस अध्यायमा यी शब्दहरू केवल परिभाषा सम्झने कुरा मात्र होइन।
वास्तविक Linux वातावरणमा command चलाएर, देखिएको जानकारी पढेर बुझ्ने अभ्यास गरिन्छ।

---

## सिकाइको प्रवाह

यस अध्यायमा तपाईंले निम्न चरणहरूमा सिक्नुहुनेछ।

1. OS भनेको के हो भनेर बुझ्ने
2. Linux kernel भनेको के हो भनेर बुझ्ने
3. Distribution भनेको के हो भनेर बुझ्ने
4. Shell भनेको के हो भनेर बुझ्ने
5. `/etc/os-release` पढेर OS जानकारी जाँच्ने
6. `uname` प्रयोग गरेर kernel जानकारी जाँच्ने
7. `/etc/os-release` र `uname` बीचको फरक बुझ्ने
8. AlmaLinux र Ubuntu बीचको फरक सोच्ने
9. जाँच command चलाएर वातावरण जानकारी मिलाउने
10. जाँचिएको जानकारी आफ्नै शब्दमा व्याख्या गर्ने

---

## 1. OS भनेको के हो

OS को पूरा रूप Operating System हो।

OS भनेको कम्प्युटरको hardware र application बीचमा बसेर सम्पूर्ण प्रणाली व्यवस्थापन गर्ने आधारभूत software हो।

OS ले उदाहरणका लागि तलका कुरा व्यवस्थापन गर्छ।

* CPU
* Memory
* Storage
* File
* Process
* User
* Network
* Input/output device

Windows, macOS, Linux आदि OS का उदाहरण हुन्।

Linux सिक्नु भनेको command मात्र कण्ठ गर्नु होइन।
OS ले कम्प्युटर कसरी व्यवस्थापन गर्छ भन्ने कुरा अवलोकन गर्नु पनि हो।

---

## 2. Linux kernel भनेको के हो

साँच्चिकै कडाइका साथ भन्नुपर्दा, Linux भन्ने शब्दले **Linux kernel** जनाउँछ।

Kernel भनेको OS को केन्द्रिय भाग हो।
यसले hardware नजिकका भागहरू व्यवस्थापन गर्छ र application वा command ले कम्प्युटर सुरक्षित रूपमा प्रयोग गर्न सक्ने बनाउँछ।

Kernel का मुख्य भूमिका उदाहरणका रूपमा:

* Process व्यवस्थापन
* Memory व्यवस्थापन
* Filesystem व्यवस्थापन
* Device व्यवस्थापन
* Network communication व्यवस्थापन

हामीले दैनिक रूपमा प्रयोग गर्ने "Linux" केवल kernel मात्र होइन।
यो kernel, command, library, package management system, configuration file आदि मिलेर बनेको हुन्छ।

---

## 3. Distribution भनेको के हो

Linux kernel मा विभिन्न software र management tools थपेर सजिलै प्रयोग गर्न मिल्ने रूपमा तयार गरिएको प्याकेजलाई **Linux distribution** भनिन्छ।

प्रमुख distribution का उदाहरणहरू:

* Ubuntu
* Debian
* AlmaLinux
* Rocky Linux
* Fedora
* Arch Linux

सबै Linux भए पनि distribution अनुसार फरक हुन्छ।

उदाहरणका लागि, package management command फरक हुन सक्छ।

| परिवार | उदाहरण | Package management |
| --- | --- | --- |
| Debian परिवार | Ubuntu, Debian | `apt` |
| Red Hat परिवार | AlmaLinux, Rocky Linux, Fedora | `dnf`, `yum` |

त्यसैले Linux प्रयोग गर्दा "Linux हो" भन्ने मात्र होइन, **कुन distribution प्रयोग भइरहेको छ** भन्ने कुरा जाँच्नु महत्त्वपूर्ण हुन्छ।

---

## 4. Shell भनेको के हो

Linux चलाउँदा हामी धेरैजसो terminal मा command टाइप गर्छौं।

यस बेला प्रयोगकर्ताले टाइप गरेको command लिने, त्यसको अर्थ बुझ्ने, र OS लाई काम गर्न अनुरोध गर्ने कार्यक्रमलाई **shell** भनिन्छ।

Shell भनेको प्रयोगकर्ता र OS बीचको interface हो।

```text
प्रयोगकर्ता
-> Shell
-> OS / Kernel
-> Hardware
```

उदाहरणका लागि, तपाईंले तलको command टाइप गर्नुभयो भने:

```bash
ls
```

Shell ले `ls` लाई बुझेर सम्बन्धित program चलाउँछ।
त्यसपछि हालको directory भित्रका file र directory को सूची देखिन्छ।

---

### Shell का प्रकारहरू

Linux मा विभिन्न प्रकारका shell प्रयोग हुन्छन्।

प्रमुख प्रकारहरू:

| Shell | विवरण |
| --- | --- |
| `sh` | आधारभूत Unix-जस्तो shell |
| `bash` | धेरै Linux वातावरणमा प्रयोग हुने प्रतिनिधि shell |
| `zsh` | completion सुविधा बलियो भएको shell |
| `fish` | प्रयोग गर्न सजिलो बनाइएको shell |

कक्षा वा शिक्षण सामग्रीमा प्रायः `bash` बढी प्रयोग गरिन्छ।

हाल प्रयोग भइरहेको shell हेर्न:

```bash
echo $SHELL
```

उदाहरण आउटपुट:

```text
/bin/bash
```

हाल चलिरहेको shell process हेर्न:

```bash
ps
```

उदाहरण आउटपुट:

```text
	PID TTY          TIME CMD
 1234 pts/0    00:00:00 bash
 1250 pts/0    00:00:00 ps
```

यो उदाहरणमा `bash` shell चलिरहेको छ भन्ने देखिन्छ।

---

### Shell र command input

Shell ले command चलाउने मात्र काम गर्दैन।

यसमा यस्ता कामहरू पनि हुन्छन्:

* Command को व्याख्या गर्ने
* Variable चलाउने
* Pipe `|` प्रयोग गरी command जोड्ने
* `>` र `>>` प्रयोग गरेर output redirect गर्ने
* Shell script चलाउने
* Command history व्यवस्थापन गर्ने

अर्थात Linux मा command-line प्रयोगको धेरै भाग shell मार्फत हुन्छ।

---

### OS, kernel, र shell को सम्बन्ध

यी तीनको सम्बन्ध यसरी बुझ्न सकिन्छ:

| शब्द | भूमिका |
| --- | --- |
| Kernel | Hardware नजिकको भाग व्यवस्थापन गर्ने OS को केन्द्र |
| Distribution | Linux kernel र विभिन्न software मिलेको package |
| Shell | प्रयोगकर्ताको command लिएर OS लाई काम गर्न अनुरोध गर्ने program |
| Terminal | Shell चलाउने स्क्रिन/अनुप्रयोग |

यहाँ महत्त्वपूर्ण कुरा: **terminal र shell एउटै होइनन्**।

Terminal भनेको अक्षर टाइप र देखाउने स्क्रिन हो।
Shell भनेको भित्र चलिरहेको command interpreter हो।

```text
Terminal
-> Shell चलाउने स्क्रिन

Shell
-> Command बुझ्ने र चलाउने program
```

यो फरक बुझ्दा Linux प्रयोग अझ स्पष्ट रूपमा व्याख्या गर्न सकिन्छ।

---

## 5. OS जानकारी जाँच्ने

Linux वातावरणमा OS र distribution सम्बन्धी जानकारी `/etc/os-release` बाट जाँच्न सकिन्छ।

```bash
cat /etc/os-release
```

उदाहरण आउटपुट:

```text
NAME="AlmaLinux"
VERSION="9.5 (Teal Serval)"
ID="almalinux"
VERSION_ID="9.5"
PLATFORM_ID="platform:el9"
PRETTY_NAME="AlmaLinux 9.5 (Teal Serval)"
```

ध्यान दिनुपर्ने मुख्य बुँदाहरू:

| Item | अर्थ |
| --- | --- |
| `NAME` | Distribution को नाम |
| `VERSION` | Version को नाम |
| `ID` | प्रणालीभित्र प्रयोग हुने पहिचान नाम |
| `VERSION_ID` | Version नम्बर |
| `PRETTY_NAME` | मानिसले सजिलै पढ्न मिल्ने नाम |

यसबाट आफूले प्रयोग गरिरहेको Linux को प्रकार बुझ्न सकिन्छ।

---

## 6. Kernel जानकारी जाँच्ने

अब kernel सम्बन्धी जानकारी जाँचौं।

```bash
uname -a
```

उदाहरण आउटपुट:

```text
Linux localhost.localdomain 5.14.0-503.el9.x86_64 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

यस परिणाममा तलका जानकारी हुन्छन्:

| जानकारी | अर्थ |
| --- | --- |
| `Linux` | Kernel नाम |
| `localhost.localdomain` | Hostname |
| `5.14.0-503.el9.x86_64` | Kernel version |
| `x86_64` | CPU architecture |
| `GNU/Linux` | OS प्रकार देखाउने जानकारी |

छोटो रूपमा हेर्न चाहनुहुन्छ भने तलका command पनि प्रयोग गर्न सकिन्छ।

```bash
uname -r
```

यसले kernel version मात्र देखाउँछ।

```bash
uname -m
```

यसले machine architecture देखाउँछ।

---

## 7. `/etc/os-release` र `uname` बीचको फरक

`/etc/os-release` र `uname` दुवै प्रणाली जानकारी जाँच्न प्रयोग हुन्छन्।
तर, यीले हेर्ने जानकारीको प्रकार फरक हुन्छ।

| Command / file | के जानकारी देखाउँछ |
| --- | --- |
| `cat /etc/os-release` | Distribution जानकारी |
| `uname -a` | Kernel जानकारी |
| `uname -r` | Kernel version |
| `uname -m` | CPU architecture |

यसलाई छोटकरीमा यसरी बुझ्न सकिन्छ।

```text
/etc/os-release
-> कुन Linux distribution हो भनेर जाँच्ने

uname
-> कुन kernel मा चलिरहेको छ भनेर जाँच्ने
```

यो फरक बुझेपछि "Linux" भन्ने शब्द अझ सही तरिकाले प्रयोग गर्न सकिन्छ।

---

## 8. AlmaLinux र Ubuntu बीचको फरक सोच्ने

AlmaLinux र Ubuntu दुवै Linux distribution हुन्।
तर तिनको परिवार र सामान्य प्रयोग क्षेत्रमा फरक हुन्छ।

| विषय | AlmaLinux | Ubuntu |
| --- | --- | --- |
| परिवार | Red Hat परिवार | Debian परिवार |
| Package management | `dnf` | `apt` |
| सामान्य प्रयोग | Server, enterprise system | Server, desktop, learning environment |
| Configuration शैली | Red Hat शैली | Debian शैली |

Linux एउटै भए पनि वातावरणअनुसार command र configuration विधि फरक हुन सक्छ।

त्यसैले tutorial वा web article पढ्दा यी कुरामा ध्यान दिनुपर्छ:

* वर्णन कुन distribution का लागि हो
* उही command आफ्नो वातावरणमा चल्छ कि चल्दैन
* Package management `apt` हो कि `dnf`
* Configuration file को स्थान उस्तै छ कि छैन

---

## 9. चलाएर हेर्नुहोस्

तलका command चलाएर परिणाम जाँच्नुहोस्।

```bash
cat /etc/os-release
uname -a
uname -r
uname -m
hostnamectl
```

`hostnamectl` बाट OS, kernel, architecture जस्ता जानकारी एकै ठाउँमा हेर्न सकिन्छ।

---

## 10. अवलोकन नोट

Command का परिणामका आधारमा तलको तालिका भरनुहोस्।

| विषय | आफ्नो वातावरण |
| --- | --- |
| Distribution नाम | |
| Version | |
| ID | |
| Kernel version | |
| Architecture | |
| Hostname | |
| Package management command | |

---

## सोचेर लेख्नुहोस्

तलका प्रश्नहरूको उत्तर आफ्नै शब्दमा दिनुहोस्।

1. OS कस्तो software हो, र यसले के व्यवस्थापन गर्छ?
2. Linux kernel भनेको के हो?
3. Linux distribution भनेको के हो?
4. `/etc/os-release` बाट के जाँच्न सकिन्छ?
5. `uname -a` बाट के जाँच्न सकिन्छ?
6. AlmaLinux र Ubuntu बीच कस्ता फरक छन्?
7. Web article वा learning material पढ्दा distribution को फरक किन ध्यान दिनुपर्छ?

---

## यस अध्यायको मुख्य बुँदा

Linux प्रयोग गर्दा "Linux" भन्ने एउटै शब्दको आधारमा वातावरणको निर्णय गर्नु उपयुक्त हुँदैन।

एउटै Linux भित्र पनि distribution, version, kernel, र package management विधि फरक हुन सक्छ।

सबैभन्दा महत्त्वपूर्ण कुरा भनेको पहिले आफ्नो वातावरण अवलोकन गर्नु र आफू कुन OS, distribution, र kernel मा काम गरिरहेको छु भनेर स्पष्ट रूपमा व्याख्या गर्न सक्नु हो।

कम्प्युटर प्रणालीको अध्ययनमा शब्द कण्ठ गर्नु मात्र पर्याप्त हुँदैन।
वास्तविक वातावरणबाट जानकारी पढ्ने क्षमता पनि अत्यन्त महत्त्वपूर्ण हुन्छ।
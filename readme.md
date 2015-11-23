## Weather ex Machina##

Στόχος του έργου είναι να κατασκευάσουμε ένα πρωτότυπο μετεωρολογικό σταθμό, ανταγωνιστικό προς τους υφιστάμενους ‘παραδοσιακούς’, μεγάλου κόστους μετεωρολογικούς σταθμούς. Ο σταθμός αυτός θα συμβάλλει στην υπέρβαση του προβλήματος διαθεσιμότητας μετεωρολογικών δεδομένων, μέσω της γεωγραφικής ανάπτυξης μεγάλου αριθμού αυτόνομων συνόλων αισθητήρων. Το υλισμικό θα είναι χαμηλού κόστους (<100€), με σύνδεση WiFi σε αστικό περιβάλλον και δυνατότητα για 2G/3G M2M για χρήση σε απομακρυσμένες περιοχές. Όλα τα δεδομένα θα συλλέγονται σε κεντρικό σύστημα σύννεφου (cloud) βασισμένο σε τεχνολογίες big data, ώστε να μπορεί να αποτελέσει μια πρώτη υποδομή για grassroot εφαρμογές smart-city.


**Ακολουθούν τα χαρακτηριστικά στα οποία στοχεύουμε:**
 - Συμπαγής, μικρού μεγέθους, εύκολης τοποθέτησης χωρίς απαραίτητη χρήση ιστού (π.χ. θα μπορούσε να κρέμεται σε ένα παράθυρο/μπαλκόνι/γωνία)
 - Mε αισθητήρες θερμοκρασίας, υγρασίας, ατμοσφαιρικής πίεσης, βροχής και αέρα. Για λόγους κόστους δε θα μετράμε βροχόπτωση, αλλά μόνο ύπαρξη βροχής με αισθητήρες σταγόνας. Αντίστοιχα δε θα μετράμε κατεύθυνση/ένταση αέρα αλλά από την κίνηση του ιδίου του σώματος του κουτιού, εφόσον κρέμεται από ένα κορδόνι, θα καταλαβαίνουμε την άπνοια ή ύπαρξη αέρα 
 - Aυτόνομο ενεργειακά, με την χρήση επαναφορτιζόμενων μπαταριών (LiPo or NiMH) που θα φορτίζουν από ένα μικρο ενσωματωμένο φωτοβολταικο
- Διασύνδεση WiFi και αποστολή δεδομένων μετρήσεων σε server μέσω (HTTP or MQTT)
 - Δυνατότητα ενημέρωσης firmware και φόρτιση μπαταρίας μέσω USB
 - Φιλικό προς DIY κατασκευαστές, συμβατό με Arduino  λογισμικό και έτοιμους αισθητήρες / modules / breakout boards
 - Δυνατότητα λειτουργίας από παραδοσιακό παραλληλεπίπεδο πλαστικό κουτί, μελέτη/προετοιμασία για περίβλημα/κουτί 3D εκτύπωσης, για οταν τα ηλεκτρονικά θα είναι σε custom PCB
 - Δυνατότητα over the Air firmware update
 - Δυνατότητα προσθήκης module για GPS/GALILEO, 3G with M2M Sim, Bluetooth
 - Δυνατότητα σύνδεσης εσωτερικής μονάδας με οθόνη για άμεση εμφάνιση των μετρήσεων


Πιο αναλυτικά οι εργασίες για αυτή την αρχική φάση του έργου είναι:

 **1. Αξιολόγηση υποψήφιου υλισμικού με υλοποίηση ελάχιστου συνδεδεμένου συστήματος (“hello IoT world” prototype)**
Έχουμε εντοπίσει αρκετές πλατφόρμες IoT με (σχεδόν) έτοιμα modules αισθητήρων, οι οποίες είναι συμβατές με arduino και φιλικές για prototyping. 

 - [TI CC3200](<https://github.com/ellak-monades-aristeias/WeatherXM/wiki/cc3200>)
 - [Spark/Particle Core](<https://github.com/ellak-monades-aristeias/WeatherXM/wiki/particle-core>)
 - [ESP8266 standalone](<https://github.com/ellak-monades-aristeias/WeatherXM/wiki/esp8266-standalone>)
 - [Atmega328 & NRF24 & ESP8266](<https://github.com/ellak-monades-aristeias/WeatherXM/wiki/ArduinoProMini_3.3.v-NRF24>)
 
Είναι εξαιρετικά δύσκολο να καταλήξει κανείς στην επιλογή μιας IoT πλατφόρμας χωρίς σε  βάθος προηγούμενη εμπειρία με τη συγκεκριμένη οικογένεια hardware/software. Οι εξελίξεις ομως στο IoT είναι τόσο ραγδαίες που πολλές πλατφόρμες πρώτο-εμφανίστηκαν στην αγορά μόλις πριν λίγους μήνες.  Για το λόγο αυτό και ακολουθώντας λογική agile, αναπτύσσουμε ένα ελάχιστο, αλλά ολοκληρωμένο σύστημα στις παραπάνω πλατφόρμες ώστε να τις αξιολογίσουμε. Το “hello IoT world” prototype είναι ένα wifi-θερμόμετρο με cloud backend (π.χ. thingspeak). Στόχος σε αυτή τη φάση είναι η αξιολόγηση και σύγκριση των πλεονεκτημάτων/μειονεκτημάτων της κάθε πλατφόρμας και η καταγραφή των διαφόρων αποτελεσμάτων (π.χ. κατανάλωση) ώστε να επιλέξουμε την ιδανικότερη με την ποια θα προχωρήσουμε. 



**2. Κατασκευή πρωτότυπου hardware**
Σε συνέχεια της αξιολόγησης και επιλογής ιδανικού hardawre, έχουμε προχωρήσουμε με την υλοποίηση των προδιαγραφών του μετεωρολογικού σταθμού, προσθέτοντας τα απαραίτητα περιφερειακά εξαρτήματα και αισθητήρες, πάνω στη βέλτιστη IoT πλατφόρμα (αποτέλεσμα προηγουμένης φάσης). Παράλληλα εμπλουτιζουμε το λογισμικό firmware  (arduino compatible) που θα διαχειρίζεται τα δεδομένα των αισθητήρων (μετεωρολογικά δεδομένα), και τα στέλνει περιοδικά σε κάποιο “ανοιχτό” cloud service  (π.χ. https://thingspeak.com/) 
([Περισσότερα](https://github.com/ellak-monades-aristeias/weatherxm/wiki/WxM-prototype))

**3. Σύνδεση hardware με backend ανοιχτό λογισμικό με δυνατότητα διαχείρισης big data**
Μέσα από προηγούμενες εμπειρίες έχουμε καταλήξει σε μια σειρά από προτεινόμενες τεχνολογίες για την διαχείριση big data όπως: Spring framework, Apache HBASE, Spark, mongoDB, Redis, Solr, etc.  οι οποίες όμως είναι αρκετά συνθέτες στη λειτουργία/εγκατάσταση. Στο opensource (CPAL-1.0) project [sitewhere.org](http://sitewhere.org) καθώς και στο [sentilo.io](http://sentilo.io) υπάρχει ήδη μια πολύ καλή διασύνδεση/integration αυτών των τεχνολογιών, καθώς και δυνατότητά για σύνδεση με arduino compatible hardware, οπότε θα κάνουμε τις απαραίτητες τροποποιήσεις στο firmware και στο server, ώστε να γίνει η σύνδεση του hardware μας με το backend για να μπορούμε να αξιοποιήσουμε τα μετεωρολογικά δεδομένα με διάφορους τρόπους, π.χ. απεικόνιση σε διαδραστικό χάρτη σε πραγματικό χρόνο, γραφήματα με ιστορικά δεδομένα, κτλ. Θα χρησιμοποιήσουμε MQTT ή HTTP πρωτόκολλο για να διευκολύνουμε και μελλοντικές διασυνδέσεις με τρίτα συστήματα ή/και άλλο IoT hardware με στόχο την δημιουργία υποδομής smart-city.
([Περισσότερα](https://github.com/ellak-monades-aristeias/WeatherXM/tree/master/D3-Backend))

**4. Μελέτη custom PCB και πρωτότυπου 3D printed πλαισίου (enclosure)**
Παράλληλα μελετάμε θέματα διάστασης/layout custom πλακέτας PCB για το hardware. Έχοντας τις τελικές διαστάσεις θα προχωρήσουμε στο σχεδιασμό custom 3d printed ABS plastic enclosure, που να μπορεί να φιλοξενήσει τους εξωτερικούς/εσωτερικούς αισθητήρες, το φωτοβολταϊκό, και τα υπόλοιπα ηλεκτρονικά, μπαταρίες κτλ.
([Περισσότερα](<https://github.com/ellak-monades-aristeias/WeatherXM/tree/master/D4-PCB-Enclosure>))

## Σε ποίους απευθύνεται - Κοινότητες Χρηστών - Προγραμματιστών(Developers) ##
To project στην παρούσα φάση του απευθύνεται σε DIY ΙοΤ & weather enthousiasts με γνώσεις hardware, electronics και embedded development, arduino. Μελλοντικές εκδόσεις θα είναι εφικτό να κατασκευαστούν απο λιγότερο τεχνικά έμπειρους χρήστες καθώς και να αποτελέσουν την βάση για (ανοιχτό) εμπορικό προϊόν χαμηλού κόστους.

## Κόστος ##
Το συνολικό κόστος του σταθμού είναι εξαιρετικά χαμηλό (λιγότερο από 100€) λαμβάνοντας υπόψιν οτι το κουτί μπορεί να εκτυπωθεί απο 3d printer. Υπάρχει μεγάλο περιθώριο περαιτέρω οικονομίας π.χ. ειδικά για τα ηλεκτρονικά εξαρτήματα αν κανείς τα προμηθευτεί  online απο κινα, μπορεί να φτάσει  ~20€. 
 

## Άδεια χρήσης ##
Τα παραδοτέα συμμορφώνονται με το Open Source Hardware Definition v1.0 με άδεια Creative Commons - Attribution - ShareAlike 3.0  για τα σχέδια/κυκλώματα. Ο κωδικάς ειναι Open Source Licensing GPL V2 

# Τελική Αναφορά

### Αριστοτέλης Συμεωνίδης
#### ΑΜ: Π2015178
#### e-mail: p15syme@ionio.gr


#### [Link Κεντρικού Αποθετηρίου](https://github.com/ioniodi/D3js-uk-political-donations)

#### [Link Προσωπικού Αποθετηρίου](https://github.com/p15syme/D3js-uk-political-donations)

#### [Link Εργασίας](https://p15syme.github.io/D3js-uk-political-donations/)

#### [Link Παραδοτέου 1](https://github.com/p15syme/D3js-uk-political-donations/tree/%CE%A02015178---%CE%A0%CE%B1%CF%81%CE%B1%CE%B4%CE%BF%CF%84%CE%AD%CE%BF-1)

#### [Link Παραδοτέου 2](https://github.com/p15syme/D3js-uk-political-donations/tree/2015178---%CE%A0%CE%B1%CF%81%CE%B1%CE%B4%CE%BF%CF%84%CE%AD%CE%BF-2)

#### [Link Εκτελέσιμου Παραδείγματος για το index.html (Avatar + Username)](https://p15syme.github.io/D3js-uk-political-donations/participants/index.html)

## Σύνοψη:

  Η παρούσα εργασίας αποτελεί επέκταση του [αποθετηρίου](https://ioniodi.github.io/D3js-uk-political-donations/full-viz.html), στην οποία χρησιμοποιώντας HTML, CSS και Javascript γίνεται οπτικοποίηση δεδομένων. Σκοπός είναι να τροποποίηση του δοσμένου παραδείγματος, έτσι ώστε να συμμορφωθεί με τα ζητούμενα των παραδοτέων που μας δίνονται. Έτσι, κάνοντας fork το αποθετήριο του ioniodi, το μετατρέπουμε στο προσωπικό μας αποθετήριο, σύμφωνα με τις οδηγίες. 

## Εισαγωγή:
  
  
### Παραδοτέο 1: Αρχικό έργο και ενδιάμεση αναφορά προόδου - 14 Μαρτίου (25%)

Υλοποιήθηκαν οι ακόλουθες ενέργειες, ώστε να ικανοποιήθουν τα ζητούμενα του Παραδοτέου 1:

* Αρχικά, τροποποίησα το URL του προσωπικού μου αποθετηρίου από https://github.com/p15syme/D3js-uk-political-donations/full-viz.html --> https://github.com/p15syme/D3js-uk-political-donations, διαγράφοντας την κατάληξη full_viz.html και αλλάζοντας την ονομασία του αρχείου full_viz.html --> index.html.
* Προσέθεσα των ήχο όταν κάνει κάποιος click στα κουμπιά, μέσω της συνάρτησης onmousedown() στη κεφαλίδα του `<ul onmousedown="bs.play()"> </ul>` .
```HTML
<script>
  var bs = new Audio();
  bs.src = "Click.mp3";
</script>
```
###### Παραδοτέο 1 - Προσθήκη ήχου στα κουμπιά.
* Χρησιμοποιώντας τα rgba και των HEX κώδικα, άλλαξα τα χρώματα από τις μπάλες. 
```Javascript
var fill = d3.scale.ordinal().range(["#F02233", "#087FBD", "#FDBB30"]); //Default
var fill = d3.scale.ordinal().range(["#D41C75", "#A9650B", "#7BB215"]); //Παραδοτέο 1
```
###### Παραδοτέο 1 - Αλλαγή χρωμάτων στα bubbles.
* Χρησιμοποιώντας τη συνάρτηση SpeechSynthesisUtterance(), εντός της συνάρτησης mouseover(), στον κώδικα του αρχείου chart.js, προσέθεσα την φωνή που θα ακούγεται για να λέει το όνομα και το ποσό του δωρήτη.
Χρησιμοποιώντας το κομμάτι του κώδικα που προσέθεσα στο αρχείο index.html, κάνω zoom στα texts της ιστοσελίδας, τοποθετώντας το class=zoom εντός των κεφαλιδών των texts.
```Javascript
	var voice = new SpeechSynthesisUtterance("Donators name is " + donor + " and the donation amount is " + amount + " pounds");
	window.speechSynthesis.speak(voice);
```
###### Παραδοτέο 1 - Όταν ο κέρσορας αγγίζει κάποιο bubble, ακούγεται το μήνυμα: Donators name is # and the donation amount is # pounds
* Προσέθεσα μία ακόμη ομαδοποίηση δεδομένων.
Έπειτα, ο κώδικας σε Javascript, όπου εισάγει το γράφημα:

  ```Javascript
  	if (name === "group-by-donation-amount")
		$("#initial-content").fadeOut(250);
		$("#value-scale").fadeOut(250);
		$("#view-donor-type").fadeOut(250);
		$("#view-party-type").fadeOut(250);
		$("#view-source-type").fadeOut(250);
		$("#view-donation-amount").fadeIn(1000);
		return donationType();
```
```Javascript
function moveToDonations(alpha) {
	return function(d) {
			var centreX;
			var centreY;
		if (d.value >= 10000000) {
			centreY = 300;
			centreX = 200;
				
		} else if (d.value < 10000000 && d.value>= 1000000) {
				centreY = 450;
				centreX = 700;
				
		} else if (d.value < 1000000 && d.value >= 500000) {
				centreY = 600;
				centreX = 200;
				
		} else  if (d.value < 500000 && d.value >= 100000) {
				centreY = 700;
				centreX = 750;
				
		} else  if (d.value <= maxVal) {
				centreY = 800;
				centreX = 200;
		}

		d.x += (centreX - d.x) * (brake + 0.06) * alpha * 1.2;
		d.y += (centreY - 100 - d.y) * (brake + 0.06) * alpha * 1.2;
	};
}
```

Και ο κώδικας σε CSS:
```CSS
#view-donation-amount {
    height: 100%;
    left: 450px;
    width: 370px;
}
#first {
    top: 50px;
}
#second{
    top: 150px;
    left: 10px;
}
#third {
    top: 335px;
    left: -80px;
}
#fourth {
    top: 480px;
    right: -80px;
}
#last {
    top: 650px;
    left: -70px;
}
```
###### Παραδοτέο 1 - Δημιουργία και οπτικοποίηση του νέου τρόπου ομαδοποίησης.

* Εντός της συνάρτησης `start()` του αρχείου chart.js προσθέτοντας το `.on("click", function(d) { window.open("http://www.google.com/search?q=" + d.donor);});`, κάνοντας κλικ πάνω σε κάποια μπάλα ο χρήστης θα κάνει αναζήτηση σε καινούργιο παράθυρο.

* Μέσω του παρακάτω κώδικα, γίνεται η μεγένθυση των λέξεων, όπως ζητήθηκε,

```HTML
.zoom:hover {
    -moz-transform: scale(2.0);
    -webkit-transform: scale(1.5);
    -o-transform: scale(2.0);
    transform: scale(1.5);
    -ms-transform: scale(2.0);
    filter: progid:DXImageTransform.Microsoft.Matrix(sizingMethod='auto expand', M11=2, M12=-0, M21=0, M22=2);
}
```
το οποίο για να χρησιμοποιηθεί και να εφαρμοστεί στην σελίδα, έγινε η προσθήκη του κομματιού `class=zoom` σε σημεία που χρειάζεται για να ικανοποιηθεί το ζητούμενο, όπως στο παράδειγμα:

```HTML
<li><a href="#" role="button" class="pure-button switch" id="all-donations">All money</a>
            </li>
```

* Τέλος, για το δεύτερο σκέλος σύμφωνα με τις οδηγίες δέσμευσα και έστειλα 5 φωτογραφίες από δωρητές στους οποίους δεν υπήρχαν και δημιούργησα ένα αρχείο 2015178.csv με τα στοιχεία μου.

#### Ενδεικτικά Στιγμιότυπα:
![ss1](https://user-images.githubusercontent.com/22681573/36947454-9c079868-1fd4-11e8-900c-df936ad26dd7.png)
###### Παραδοτέο 1 - Μεγέθυνση των γραμμάτων.
![ss2](https://user-images.githubusercontent.com/22681573/36947455-9d7662c4-1fd4-11e8-9b3d-8409cda8c857.png)
###### Παραδοτέο 1 - Νέος Τρόπος Ομαδοποίησης.

### Παραδοτέο 2: Τελικό έργο και τελική αναφορά (25%), 9 Μαΐου

  Για το Παραδοτέο 2 έγιναν οι εξής αλλαγές:
  
* Τροποποιήθηκε ο κώδικας του αρχείου *chart.js*, προσθέτωντας το παρακάτω block κώδικα, με αποτέλεσμα την εμφάνιση της εικόνας του δωρητή, όταν ο χρήστης κάνει hove over από το bubble που τον αντιπροσωπεύει:
```Javascript
var infoPic = document.createElement("img");
    infoPic.setAttribute("src","http://www.bizreport.com/2011/02/03/android-logo-200x200.jpg");
    infoPic.setAttribute("height","42");
    infoPic.setAttribute("width","42");
    infoPic.setAttribute("onerror",'this.src=\"https://github.com/favicon.ico\";');
    document.getElementById("cssPic").insertBefore(infoPic,document.getElementById("cssPic").firstChild);
    infoPic.src = imageFile;
```
###### Παραδοτέο 2 - Εμφάνιση του ιστορικού

* Στο φάκελο *participants* τροποποίησα το αρχείο *index.html*, στην θέση *position #015*, χρησιμοποιώντας το ακόλουθο block κώδικα, με σκοπό την εμφάνιση των στοιχείων μου(github username & picture). Όσον αναφορά το συγκεκριμένο ερώτημα, στο κεντρικο αποθετήριο παρουσιάζεται με λάθος μορφή από'τι στο αρχείο του προσωπικού μου αποθετηρίου, χωρίς να έχω βρει τον τρόπο να το φτιάξω:

```
<div style="border: 2px solid; border-radius: 5px; background-color: #4267B2; width: fit-content; float: left; margin: 10px 10px 10px 10px;">
      <h4>
        <span>&nbsp;</span>
        <img src="https://avatars2.githubusercontent.com/u/22681573?s=400&v=4" height="42" width="42">
        <span class="ml1"><span class="letters">&nbsp;p15syme&nbsp;</span></span>
      </h4>
  </div>
  
  <script>
  // Wrap every letter in a span
  $('.ml1 .letters').each(function(){
    $(this).html($(this).text().replace(/([^\x00-\x80]|\w)/g, "<span class='letter'>$&</span>"));
  });
   
   anime.timeline({loop: true}) 
    .add({
    targets: '.ml1 .letters',
    scale: [0,1],
    opacity: [0,1],
    easing: "easeOutElastic",
    duration: 2000,
    delay: function(el, i, l) {
      return 750 * (i+2);
    }
  }).add({
    targets: '.ml1',
    opacity: 0,
    duration: 1000,
    easing: "easeInOutQuint",
    delay: 1000
  });    
  </script>
```
* https://p15syme.github.io/D3js-uk-political-donations/participants/index.html To link στο εκτελέσιμο παράδειγμα του προσωπικού μουθ παραδείγματος.
###### Παραδοτέο 2 - Εμφάνιση του ονόματος και του avatar στο αρχείο index.html
* Στο τελευταίο ζητούμενο που έκανα για το Παραδοτέο 2, ζητούσε να δημιουργήσουμε μία σελίδα, όπου θα αντλούσε στοιχεία δυναμικά από το κεντρικό αποθετήριο του ioniodi, μέσω της σελίδας Insights. Έτσι, δημιούργησα το αρχείο 2015178.html. Η άντληση των δεδομένων έγινε μέσω XML HTTP Request.

#### Ενδεικτικά Στιγμιότυπα Παραδοτέου 2:

![ss3](https://user-images.githubusercontent.com/22681573/39723986-236abab2-5250-11e8-9964-7880b1afc77f.png)
###### Παραδοτέο 2 - Εμφάνιση του ιστορικού.

![ss4](https://user-images.githubusercontent.com/22681573/39724154-a397d4d6-5250-11e8-9a30-4076c76eed12.png)
###### Παραδοτέο 2 - Η σελίδα στην οποία φαίνονται τα contributions από τους χρήστες του κεντρικού απεθετηρίου.

![ss5](https://user-images.githubusercontent.com/22681573/39724156-a3c569b4-5250-11e8-8990-3f3b4229c207.png)
###### Παραδοτέο 2 - Εμφάνιση του ιστορικού.

![ss6](https://user-images.githubusercontent.com/22681573/39814294-6d654bb2-539c-11e8-8e4b-5d067c8fb94d.gif)
###### Παραδοτέο 2 - GIF, όπου δείχνει το τρόπο εμφάνισης των στοιχείων μου στο εκτελέσιμο αρχείο index.html στο προσωπικό μου αποθετήριο.

## Μέθοδοι - Τεχνικές: 

  Για τη περίπτωση των ζητουμένων και των δύο παραδοτέων, χρησιμοποιήθηκε το *Sublime Text Editor*, με το οποίο επεξεργάστηκα τους κώδικους των αρχείων *index.html, chart.js, style.css* και δοκιμάζονταν τοπικά, αλλά και μέσω του GitHub. Έπειτα, χρησιμοποίησα και τα εργάλεια για προγραμματιστές που διαθέτει το Mozilla Firefox, για να βλέπω αν ο κώδικας μου τρέχει σωστά.
  
## Εργαλεία:

  Για την ολοκλήρωση των ζητουμένων από τα δύο παραδοτέαμ χρησιμοποίησα τα ακόλουθα εργαλεία:
  * Την εφαρμογή *Ζωγραφική*.
  * Το GIMP.
  * Sublime Text Editor.
  * ScreenToGif

## Συμπεράσματα:

  Συνοψίζοντας, η εργασία που μας ανατέθηκε για το μάθημα Τεχνολογίες Λογισμικού, μας βρίσκει αντιμέτωπους με μία σειρά από διάφορα ερωτήματα, στα οποία για να απαντήσουμε πρέπει να απαντηθούν με  κομμάτια κώδικα σε HTML, CSS και Javascript, χρησιμοποιώντας την βιβλιοθήκη D3js. Στη περίπτωση του δεύτερου παραδοτέου, χρειάστηκε να δημιουργηθεί καινούργια σελίδα σε HTML. Έτσι, συμπεραίνουμε ότι η συγκεκριμένη εργασία, αποτέλεσε έναν πολύ ενδιαφέρον τρόπο να ασχοληθούμε με την αναπαράσταση γραφημάτων, μέσω της βιβλιοθήκης D3js, όπου μπορούμε να αντλούμε δυναμικά δεδομένα από ενα αρχείο .csv, μέσω της σελίδας. Επιπρόσθετα, μέσω του δεύτερου σκέλους του δεύτερου παραδοτέου, μαθαίνουμε πώς να αντλούμε δεδομένα από ένα δημόσιο αποθετήριο μέσω του τμήματος *Insights*. Ουσιαστικά αποτελεί ένα μέσο, από το οποίο ο φοιτητής έρχεται σε επαφή με HTML, CSS, Javascript, όπου και να πειραματιστεί, αλλά και να συναντήσει ορισμένες απαιτητικές προκλήσεις, ιδιαίτερα αν έχει γνώσεις αρχάριου επιπέδου για τις παραπάνω γλώσσες.

## Βιβλιογραφία:

##### [GitHub API Statistics](https://developer.github.com/v3/repos/statistics/)

##### [XML HTTP Request (1)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data)

##### [XML HTTP Request (2)](https://www.w3schools.com/xml/ajax_applications.asp)

##### [Display Image in Javascript](https://stackoverflow.com/questions/5451445/how-to-display-image-with-javascript)

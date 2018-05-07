# Τελική Αναφορά

### Αριστοτέλης Συμεωνίδης
#### ΑΜ: Π2015178
#### e-mail: p15syme@ionio.gr


#### [Link Κεντρικού Αποθετηρίου](https://github.com/ioniodi/D3js-uk-political-donations)

#### [Link Προσωπικού Αποθετηρίου](https://github.com/p15syme/D3js-uk-political-donations)

#### [Link Εργασίας](https://p15syme.github.io/D3js-uk-political-donations/)

#### [Link Παραδοτέου 1](https://github.com/p15syme/D3js-uk-political-donations/tree/%CE%A02015178---%CE%A0%CE%B1%CF%81%CE%B1%CE%B4%CE%BF%CF%84%CE%AD%CE%BF-1)

#### [Link Παραδοτέου 2](https://github.com/p15syme/D3js-uk-political-donations/tree/2015178---%CE%A0%CE%B1%CF%81%CE%B1%CE%B4%CE%BF%CF%84%CE%AD%CE%BF-2)

## Σύνοψη:

  Η παρούσα εργασίας αποτελεί επέκταση του [αποθετηρίου](https://ioniodi.github.io/D3js-uk-political-donations/full-viz.html), στην οποία χρησιμοποιώντας HTML, CSS και Javascript γίνεται οπτικοποίηση δεδομένων. Σκοπός είναι να τροποποίηση του δοσμένου παραδείγματος, έτσι ώστε να συμμορφωθεί με τα ζητούμενα των παραδοτέων που μας δίνονται. Έτσι, κάνοντας fork το αποθετήριο του ioniodi, το μετατρέπουμε στο προσωπικό μας αποθετήριο, σύμφωνα με τις οδηγίες. 
  
  
## Παραδοτέο 1: Αρχικό έργο και ενδιάμεση αναφορά προόδου - 14 Μαρτίου (25%)

Υλοποιήθηκαν οι ακόλουθες ενέργειες, ώστε να ικανοποιήθουν τα ζητούμενα του Παραδοτέου 1:

* Αρχικά, τροποποίησα το URL του προσωπικού μου αποθετηρίου από https://github.com/p15syme/D3js-uk-political-donations/full-viz.html --> https://github.com/p15syme/D3js-uk-political-donations, διαγράφοντας την κατάληξη full_viz.html και αλλάζοντας την ονομασία του αρχείου full_viz.html --> index.html.
* Προσέθεσα των ήχο όταν κάνει κάποιος click στα κουμπιά, μέσω της συνάρτησης onmousedown() στη κεφαλίδα του `<ul onmousedown="bs.play()"> </ul>` .
```HTML
<script>
  var bs = new Audio();
  bs.src = "Click.mp3";
</script>
```

* Χρησιμοποιώντας τα rgba και των HEX κώδικα, άλλαξα τα χρώματα από τις μπάλες. 
```Javascript
var fill = d3.scale.ordinal().range(["#F02233", "#087FBD", "#FDBB30"]); //Default
var fill = d3.scale.ordinal().range(["#D41C75", "#A9650B", "#7BB215"]); //Παραδοτέο 1
```

* Χρησιμοποιώντας τη συνάρτηση SpeechSynthesisUtterance(), εντός της συνάρτησης mouseover(), στον κώδικα του αρχείου chart.js, προσέθεσα την φωνή που θα ακούγεται για να λέει το όνομα και το ποσό του δωρήτη.
Χρησιμοποιώντας το κομμάτι του κώδικα που προσέθεσα στο αρχείο index.html, κάνω zoom στα texts της ιστοσελίδας, τοποθετώντας το class=zoom εντός των κεφαλιδών των texts.
```Javascript
	var voice = new SpeechSynthesisUtterance("Donators name is " + donor + " and the donation amount is " + amount + " pounds");
	window.speechSynthesis.speak(voice);
```

* Προσέθεσα μία ακόμη ομαδοποίηση δεδομένων.
  Αρχικά, το κουμπί για τη μετάβαση από την αρχική σελίδα στον καινούργιο τρόπο ομαδοποίησης.
```
 <li><a href="#" role="button" class="pure-button switch" id="group-by-donation-amount">Split by the amount of the donation</a>
 </li> 
```

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

* Εντός της συνάρτησης `start()` του αρχείου chart.js προσθέτοντας το `.on("click", function(d) { window.open("http://www.google.com/search?q=" + d.donor);});`, κάνοντας κλικ πάνω σε κάποια μπάλα ο χρήστης θα κάνει αναζήτηση σε καινούργιο παράθυρο.

* Τέλος, για το δεύτερο σκέλος σύμφωνα με τις οδηγίες δέσμευσα και έστειλα 5 φωτογραφίες από δωρητές στους οποίους δεν υπήρχαν και δημιούργησα ένα αρχείο 2015178.csv με τα στοιχεία μου.

### Ενδεικτικά Στιγμιότυπα:
![ss1](https://user-images.githubusercontent.com/22681573/36947454-9c079868-1fd4-11e8-900c-df936ad26dd7.png)
![ss2](https://user-images.githubusercontent.com/22681573/36947455-9d7662c4-1fd4-11e8-9b3d-8409cda8c857.png)

## Παραδοτέο 2: Τελικό έργο και τελική αναφορά (25%), 9 Μαΐου

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

* Στο φάκελο *participants* τροποποίησα το αρχείο *index.html*, στην θέση *position #015*, χρησιμοποιώντας το ακόλουθο block κώδικα, με σκοπό την εμφάνιση των στοιχείων μου(github username & picture):
```
<div style="border: 2px solid; border-radius: 5px; background-color: #4267B2; width: fit-content; float: left; margin: 10px 10px 10px 10px;">
      <h4>
        <span>&nbsp;</span>
        **<img src="https://avatars2.githubusercontent.com/u/22681573?s=400&v=4" height="42" width="42">**
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

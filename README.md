<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>repl.it</title>
    <link href="style.css" rel="stylesheet" type="text/css" />
  </head>
  <body>

    <form>
      <!--Page titre-->
      <h1>Magasin d'électronique</h1>

      <!--Courte description de mon entreprise-->
      <p>A notre magasin on vous vent seulement des item de meilleur qualité. On fait sur que vous etre satisfait avec vos achat. Quand vous acheter a notre magasin vous aller recevoir vos item la jour d'apres!</p>

      <!--Bouton radio qui determine si l'utilisateur vie au Quebec ou Ontario-->
      <p>Est tu situe en: </p>
      <label for = "tax"></label>
      <input type = "radio" name = "province" value = "Ontario"/>Ontario
      <input type = "radio" name = "province" value = "Quebec"/>Quebec


      <br><br>

      <!--Checkbox pour les item que l'utilisateur -->
      <label for="listItem"></label><br>
      
      <input type="checkbox" id="listItem" name="item" value="Clavier 12.75$"/>Clavier 12.75$<br>
       <img src = "https://www.numerama.com/content/uploads/2017/03/1100574-1100574_4.jpg" alt = "Clavier" width="200"><br>
      
      
      <input type="checkbox" id="listItem" name="item" value="Souris 9.35$"/>Souris 9.35$<br>
      <img src = "https://assets2.razerzone.com/images/pnx.assets/89b592e45a60be05a671c021f3363ac0/razer-mamba-elite_500x500.png" alt = "Souris" width="200"><br>
      
      
      <input type="checkbox" id="listItem" name="item" value="Écran 79.99$"/>Écran 79.99$<br>
      <img src = "https://www.renderhub.com/ross-hankinson/computer-monitor-screen/computer-monitor-screen-01.jpg" alt = "Écran" width="200"><br>
      
      
      <input type="checkbox" id="listItem" name="item" value="USB flash drive 57.25$"/>USB flash drive 57.25$<br>
      <img src = "https://cdn.ttgtmedia.com/rms/onlineImages/150331_storage_USB_mobile.jpg" alt = "USB Flash drive" width="200"><br>
      
      
      <input type="checkbox" id="listItem" name="item" value="Camera web 44.75$"/>Camera web 44.75$<br>
      <img src = "https://webobjects2.cdw.com/is/image/CDW/6256981?$product-main$" alt = "Camera web" width="200"><br>


    <!--Le bouton qui soummet les achats-->
    <input type="button" id="btnSoumet" onclick="recus()"  value="Passer a la caisse"/><br><br>

    <!--ou on affiche les achats/recus-->
    <div id="divAffiche">
    </div>
      
    
    
    <script>
      /*La tax de l'Ontario*/
      const taxOnt = 1.13;
      /*La tax du Quebec*/
      const taxQueb  = 1.15;

      /*declare la variable de le prix total*/
      var prixTotal = 0;

      /*Fonction que l'on utilise pour afficher le recus*/
      function recus(){
      
      /*appel au div "affiche"*/
      var affiche = document.getElementById("divAffiche");

      /*cherche le quel des bouton radio a ete choisi*/
      var proChoi = document.getElementsByName("province");

      var pro = ""
            for (var i = 0; i < proChoi.length; i++) {
              if (proChoi[i].checked) {
                  pro = proChoi[i].value;
              }
            }

        /*cherche pour les checkbox qui a ete choisi*/
        var itemChoi = document.getElementsByName("item");

        /*declare la variable ou la list d'item vas etre placer*/
        var messageList = "";
        
        var numLi = 0;
        for (var i=0; i < itemChoi.length; i++) {
              if (itemChoi[i].checked) {
                
                numLi = numLi + 1 //numero de list

                /*Construire la list*/
                messageList += numLi + "." + itemChoi[i].value + "<br>" ;
              }
            }

        /*Les calcule du prix total avec tax si l'utilisateur vie en Ontario*/
        if(pro == "Ontario"){
          if (itemChoi[0].checked){
            prixTotal = prixTotal + (12.75 * taxOnt);

          }
          if (itemChoi[1].checked){
            prixTotal = prixTotal + (9.35 * taxOnt);

          }
          if (itemChoi[2].checked){
            prixTotal = prixTotal + (79.99 * taxOnt);
          }
          if (itemChoi[3].checked){
            prixTotal = prixTotal + (57.25 * taxOnt);

          }
          if (itemChoi[4].checked){
            prixTotal = prixTotal + (44.75 * taxOnt);

          }
        /*Les calcule du prix total avec tax si l'utilisateur vie au Quebec*/
        }else if (pro == "Quebec"){
          if (itemChoi[0].checked){
            prixTotal = prixTotal + (12.75 * taxQueb);

          }
          if (itemChoi[1].checked){
            prixTotal = prixTotal + (9.35 * taxQueb);

          }
          if (itemChoi[2].checked){
            prixTotal = prixTotal + (79.99 * taxQueb);
          }
          if (itemChoi[3].checked){
            prixTotal = prixTotal + (57.25 * taxQueb);

          }
          if (itemChoi[4].checked){
            prixTotal = prixTotal + (44.75 * taxQueb);

          }
        }


      /*declare des variable*/  
      var sousPrix = 0;
      var taxPrixTotal = 0;

      /*on calcule les prix sans tax pour l'Ontario*/
      if (pro == "Ontario"){
        sousPrix = prixTotal/taxOnt;
        taxPrixTotal = sousPrix*0.13;
      
      /*on calcule les prix sans tax pour le Quebec*/
      }else if (pro == "Quebec"){
        sousPrix = prixTotal/taxQueb;
        taxPrixTotal = sousPrix*0.15;
      }
        
      /*Arrondie les prix au centieme pres*/
        prixTotal = prixTotal.toFixed(2)
        prixTotal = prixTotal + "$"

        sousPrix = sousPrix.toFixed(2)
        sousPrix = sousPrix + "$"

        taxPrixTotal = taxPrixTotal.toFixed(2)
        taxPrixTotal = taxPrixTotal + "$"

      /*recus si l'utilisateur vie en Ontario*/
      if (pro == "Ontario"){
        var recusFinal = [
        ['RECUS','<br>'],
        [messageList],
        ['-----------------------','<br>'],
        ['Sous prix:',sousPrix,'<br>'],
        ['Taxes (ON 13%):',taxPrixTotal,'<br>'],
        ['Total:',prixTotal,'<br>']];

      /*recus si l'utilisateur vie au Quebec*/
      }else if (pro == "Quebec"){
        var recusFinal = [
        ['RECUS','<br>'],
        [messageList],
        ['-----------------------','<br>'],
        ['Sous prix:',sousPrix,'<br>'],
        ['Taxes (ON 15%):',taxPrixTotal,'<br>'],
        ['Total:',prixTotal,'<br>']];

      }



        /*affiche le recus*/
        affiche.innerHTML = recusFinal.join('\n');
    
      
      
        
      }

      </script>
    </form>
  </body>
</html>


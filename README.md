<html>
	<body>
		

	<h1>Hello Incapsulate...!</h1>
    
    <h5> welcome to blackjack...</h5>
    
    
    <p id='text-area'></p>
    
    <button id = 'new-game-button'>New game!</button>
    <button id ='hit-button'>Hit!</button>
    <button id='stay-button'>Stay</button>
	
	<script>
		

			let suits = ['Heart', 'Diamond','Club','Spades'];
			let values= ['Ace','Two','Three','Four','Five','Six','Seven','Eight','Nine','Ten','Jack','Queen','King'];

			let textArea = document.getElementById("text-area");
			let newGameButton = document.getElementById("new-game-button");
			let hitButton = document.getElementById("hit-button");
			let stayButton= document.getElementById("stay-button");

			let gameStarted = false, gameOver = false, playerWon = false, dealerCards = [],
			playerCards = [], dealerScore = 0, playerScore = 0, deck = [];


			hitButton.style.display = 'none';
			stayButton.style.display = 'none';

			newGameButton.addEventListener('click', function(){
			  
				deck  = createDeck(); 
			    shuffleDeck(deck);
				playerCards = [getNextCard(), getNextCard()];
				dealerCards=  [getNextCard(), getNextCard()];
				gameStarted = true;

			  textArea.innerText = 'Started..'; 
			  newGameButton.style.display = 'none';
			  hitButton.style.display = 'inline';
			  stayButton.style.display = 'inline';
			  showStatus();
			});

			    function createDeck()
			    {
			     let deck = [];
			      
			      for (let i = 0; i < suits.length; i++) {
							for (let j = 0; j < values.length; j++) {
								
								let card = {
								  suit : suits[i],
								  value : values[j]
								};
								deck.push(card);
							}
						}
			      return deck;
			    }
			  /*  new   */

			  hitButton.addEventListener('click', function(){
			  	alert('hii..');
					 playerCards.push(getNextCard());
					 checkForEndOfGame();
					 showStatus();
				});

			stayButton.addEventListener('click', function(){
			 gameOver = true;
			 checkForEndOfGame();
			 showStatus();
			});

				function checkForEndOfGame(){
				 updateScores();

				 if(gameOver){
				   while(dealerScore<playerScore && playerScore <=21 && dealerScore <=21){
				           dealerCards.push(getNextCard());
				           updateScores();
				   }
				 }

				   if(playerScore>21){
				     playerWon=false;
				     gameOver = true;
				   }

				   else if(dealerScore>21){
				     playerWon = true;
				     gameOver = true;
				   }

				   else if(gameOver){
				     if(playerScore>dealerScore){
				       playerWon = true;
				     }
				     else{
				       playerWon = false;
				     }
				   }
				}
			  	/*endd  */

			  
			  
			  function getCardString(card){
			    return card.value + ' of ' + card.suit;
			  }
			  
			  function getNextCard(){
			    return deck.shift();
			  }
			  
			  function getCardNumericValue(card) {
			    
			    switch (card.value) {
			      case 'Ace':
			        return 1;      
			      case 'Two' :
			        return 2;
			      case 'Three' :
			        return 3;
			      case 'Four' :
			        return 4;
			      case 'Five' :
			        return 5;
			      case 'Six' :
			        return 6;
			      case 'Seven' :
			        return 7;
			      case 'Eight' :
			        return 8;
			      case 'Nine' :
			        return 9;
			      default:
			         return 10;
			    }
			  }
			  
			  function getScore(cardArray)
			  { 
			    
			    let score = 0;
			    let hasAce = false;
			    
			    for(let i=0; i< cardArray.length ; i++){
			      let card = cardArray[i];
			      score += getCardNumericValue(card);
			      if(card.value === 'Ace'){
			        hasAce = true;
			      }
			    }
			    if(hasAce && score+ 10 <= 21){
			        return score +10;
			      }
			      return score; 
			  }
			  
			  function updateScores(){
			    dealerScore = getScore(dealerCards);
			    playerScore = getScore(playerCards);
			  }
			  
			  
			  function showStatus() {
					 if(!gameStarted){
					      textArea.innerText = 'welcome dear....';
					      return;
					    }
					    
					   let dealerCardString ='';
					   for(let i=0; i< dealerCards.length ; i++){
					      
					     dealerCardString += getCardString(dealerCards[i]) + '\n'
					   }
					   
					   let playerCardString ='';
					   for(let i=0; i< playerCards.length ; i++){
					     
					     playesrCardString += getCardString(playerCards[i]) + '\n'
					   }
					   
					   updateScores();
					   
					   textArea.innerText = 
					   'dealer has :\n' +
					   dealerCardString +
					   '( Score ' + dealerScore + ' )\n\n';
					   
					    'player has :\n' +
					   playerCardString +
					   '( Score ' + playerScore + ' )\n\n';
					   
					   if(gameOver){
					     
						     if(playerWon){
						       textArea.innerText += 'YOU WIN';
						     }
						     else {
						       textArea.innerText += 'DEALER WINS';
						     }
						     
						      newGameButton.style.display = 'inline';
						      hitButton.style.display = 'none';
						      stayButton.style.display = 'none';
					   }
		
			  	}
			  
			  function shuffleDeck(deck){
			       for (let i =0 ;i < deck.length ; i++) {
			         
			         let swpIdx = Math.trunc( Math.random() * deck.length);
			         let temp = deck[swpIdx];
			         deck[swpIdx] = deck[i];
			         deck[i] = temp;
			       }
			      
			  }
		
	</script>
</body>
</html>

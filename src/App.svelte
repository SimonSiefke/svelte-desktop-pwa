<script>
const images = ['images/fox1.jpg','images/fox2.jpg','images/fox3.jpg','images/fox4.jpg'];

let src = images[0];

setInterval(()=> {
  src = randomValueFromArray(images);
}, 2000)

function randomValueFromArray(array) {
  let randomNo =  Math.floor(Math.random() * array.length);
  return array[randomNo];
}

let deferredPrompt;
let addBtnDisplay='none'

window.addEventListener('beforeinstallprompt', (e) => {
  // Prevent Chrome 67 and earlier from automatically showing the prompt
  e.preventDefault();
  // Stash the event so it can be triggered later.
  deferredPrompt = e;
  // Update UI to notify the user they can add to home screen
  addBtnDisplay = 'block';

  document.querySelector('button').addEventListener('click', (e) => {
		console.log('click')
    // hide our user interface that shows our A2HS button
    addBtnDisplay = 'none';
    // Show the prompt
    deferredPrompt.prompt();
    // Wait for the user to respond to the prompt
    deferredPrompt.userChoice.then((choiceResult) => {
        if (choiceResult.outcome === 'accepted') {
          console.log('User accepted the A2HS prompt');
        } else {
          console.log('User dismissed the A2HS prompt');
        }
        deferredPrompt = null;
      });
  });
});


</script>

<style>
img{
	max-width: 100%
}
</style>

<img {src} alt="a fox picture">
<button style="display: {addBtnDisplay}">Add to home screen</button>

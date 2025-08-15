<div id="interaction-container" style="font-family:sans-serif; text-align:center; margin-top:50px;padding: 80;border-radius: 20; background-color: purple;">
  <div id="step-text"></div>
  <div id="button-container" style="margin-top:20px;"></div>
  <div id="fingerprint-container" style="margin-top:30px; display:none;">
    <div id="fingerprint" style="width:100px; height:100px; margin:0 auto; background:#ddd; border-radius:50%; line-height:100px; cursor:pointer; font-size:40px;">🤚</div>
    <div id="fingerprint-message" style="margin-top:10px;"></div>
  </div>
</div>

<script>
const steps = {
  1: "Hi, I'm Bernard. Do you know me?",
  z: "Well, I'm a young sexy nigga, that's all you need to know.",
  2: "Good. So my birthday is next week Wednesday and I don't want a 'king is born' message. Do you understand?",
  3: "What I want is two baddies with big yansh from you. Will you do this for me?",
  4: "Good. Sign the contract.",
  5: "Send me a message on WhatsApp."
};

let currentStep = 1;

function showStep(step) {
  const container = document.getElementById('step-text');
  const buttons = document.getElementById('button-container');
  const fingerprintContainer = document.getElementById('fingerprint-container');

  fingerprintContainer.style.display = 'none';
  
  if(step === 1){
    container.innerHTML = steps[1];
    buttons.innerHTML = `
      <button id="yesBtn" style="padding:10px 20px; margin:5px; background:#4CAF50; color:white; border:none; border-radius:5px; cursor:pointer;">Yes</button>
      <button id="noBtn" style="padding:10px 20px; margin:5px; background:#f44336; color:white; border:none; border-radius:5px; cursor:pointer;">No</button>
    `;
    document.getElementById('yesBtn').onclick = () => { currentStep = 2; showStep(currentStep); };
    document.getElementById('noBtn').onclick = () => { currentStep = 'z'; showStep(currentStep); };
  } 
  else if(step === 'z'){
    container.innerHTML = steps['z'];
    buttons.innerHTML = `<button id="proceedBtn" style="padding:10px 20px; margin:5px; background:#4CAF50; color:white; border:none; border-radius:5px; cursor:pointer;">Proceed</button>`;
    document.getElementById('proceedBtn').onclick = () => { currentStep = 2; showStep(currentStep); };
  }
  else if(step === 2 || step === 3){
    container.innerHTML = steps[step];
    buttons.innerHTML = `
      <button id="yesBtn" style="padding:10px 20px; margin:5px; background:#4CAF50; color:white; border:none; border-radius:5px; cursor:pointer;">Yes</button>
      <button id="noBtn" style="padding:10px 20px; margin:5px; background:#f44336; color:white; border:none; border-radius:5px; cursor:pointer;">No</button>
    `;
    document.getElementById('yesBtn').onclick = () => { currentStep = step + 1; showStep(currentStep); };
    document.getElementById('noBtn').onclick = () => { alert("No is not allowed! Click Yes to proceed."); };
  }
  else if(step === 4){
    container.innerHTML = steps[4];
    buttons.innerHTML = '';
    fingerprintContainer.style.display = 'block';
    const fingerprint = document.getElementById('fingerprint');
    const msg = document.getElementById('fingerprint-message');

    fingerprint.onmousedown = fingerprint.ontouchstart = () => {
      msg.innerHTML = "Hold for 3 seconds...";
      setTimeout(() => {
        msg.innerHTML = "Success! Proceed to WhatsApp.";
        currentStep = 5;
        showWhatsAppStep();
      }, 3000);
    };
  }
}

function showWhatsAppStep(){
  const container = document.getElementById('step-text');
  const buttons = document.getElementById('button-container');
  const fingerprintContainer = document.getElementById('fingerprint-container');

  fingerprintContainer.style.display = 'none';
  container.innerHTML = steps[5];
  buttons.innerHTML = `<a href="https://wa.me/2349040615298" target="_blank">
                         <button style="padding:10px 20px; background:#25D366; color:white; border:none; border-radius:5px; cursor:pointer;">Message on WhatsApp</button>
                       </a>`;
}

showStep(currentStep);
</script>

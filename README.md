# mass-unfollow-instagram-users
Unfollow instagram users - No app needed

Go to your profile on instagram.com (sign in if not already)
Click on XXX following for the popup with the users you're following to appear.
Open Chrome Devtools and Paste the following into the Console and hit return. - [If you get pasting is disabled type 'allow pasteing' and press enter.

(async function(){
  const UNFOLLOW_LIMIT = 800;
  const delay = (ms) => new Promise(res => setTimeout(res, ms));
  const findButton = (txt) => [...document.querySelectorAll("button")].find(btn => btn.textContent.includes(txt));

  console.log("Start");
  for (let i = 0; i < UNFOLLOW_LIMIT; i++) {
    const $next = findButton("Following");
    if (!$next) {
      console.log("No more 'Following' buttons found.");
      break;
    }
    
    $next.scrollIntoView({behavior: "smooth", block: "center"});
    $next.click();
    await delay(1000);

    let $confirm = findButton("Unfollow");
    if ($confirm) {
      $confirm.click();
      console.log(`Unfollowed #${i+1}`);
    } else {
      console.log("Unfollow confirmation button not found.");
    }

    await delay(20000); // 20 seconds delay
  }

  console.log("Finished unfollowing.");
})();

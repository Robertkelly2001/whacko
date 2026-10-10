# whacko
same again whack a mole classic with harder levels the better you do 
        finishGame();
        return;
      }
    }
    requestAnimationFrame(loop);
  }

  function finishGame() {
    running=false;
    paused=false;
    const isRecord=score>best;
    if(isRecord) {
      best=score;
      save(BEST_KEY,best);
    }
    holes.forEach(h=>{
      h.active=false;
      h.el.classList.remove("active");
    });
    $("finalScore").textContent=score;
    $("finalBest").textContent=best;
    $("titleBest").textContent=best;
    $("newRecord").hidden=!isRecord;
    $("endMessage").textContent=
      score>=75?"LEGENDARY MOLE MASTER, "+player.toUpperCase()+"!":
      score>=40?"INCREDIBLE WORK, "+player.toUpperCase()+"!":
      score>=20?"NICE WHACKING, "+player.toUpperCase()+"!":
      "KEEP PRACTISING, "+player.toUpperCase()+"!";
    show("gameOver");
    soundEnd();
  }

  function togglePause() {
    if(!running) return;
    paused=!paused;
    if(paused){
      show("pauseOverlay");
    }else{
      show("none");
      lastFrame=0;
    }
  }

  // Touch, pen and mouse swiping.
  // Each target can only score once per continuous swipe.
  function hitAt(x,y){
    const target=document.elementFromPoint(x,y);
    const hole=target?.closest(".hole");
    if(!hole) return;
    const index=holes.findIndex(h=>h.el===hole);
    if(index>=0 && !pointerHits.has(index)){
      pointerHits.add(index);
      whack(index);
    }
  }

  board.addEventListener("pointerdown",e=>{
    if(!running||paused) return;
    e.preventDefault();
    initAudio();
    pointerHeld=true;
    pointerHits.clear();
    try{board.setPointerCapture(e.pointerId)}catch{}
    hitAt(e.clientX,e.clientY);
  });

  board.addEventListener("pointermove",e=>{
    if(!pointerHeld) return;
    e.preventDefault();
    hitAt(e.clientX,e.clientY);
  });

  function releasePointer(){
    pointerHeld=false;
    pointerHits.clear();
  }
  board.addEventListener("pointerup",releasePointer);
  board.addEventListener("pointercancel",releasePointer);
  window.addEventListener("blur",()=>{
    releasePointer();
    if(running&&!paused) togglePause();
  });

  // Keyboard layout:
  // 1 2 3
  // 4 5 6
  // 7 8 9
  // Also supports Q W E / A S D / Z X C.
  const keyMap={
    "1":0,"2":1,"3":2,
    "4":3,"5":4,"6":5,
    "7":6,"8":7,"9":8,
    q:0,w:1,e:2,
    a:3,s:4,d:5,
    z:6,x:7,c:8
  };

  document.addEventListener("keydown",e=>{
    if(document.activeElement===$("nameInput")){
      if(e.key==="Enter") {
        e.preventDefault();
        $("nameInput").blur();
        startGame();
      }
      return;
    }
    if(e.repeat) return;
    const key=e.key.toLowerCase();
    if(key==="escape"||key==="p"){
      if(running){
        e.preventDefault();
        togglePause();
      }
      return;
    }
    if(key in keyMap && running && !paused){
      e.preventDefault();
      initAudio();
      whack(keyMap[key]);
    }
  });

  $("playBtn").addEventListener("click",startGame);
  $("againBtn").addEventListener("click",startGame);
  $("pauseBtn").addEventListener("click",togglePause);
  $("resumeBtn").addEventListener("click",togglePause);
  $("menuBtn").addEventListener("click",()=>{
    running=false;
    paused=false;
    $("titleBest").textContent=best;
    show("titleScreen");
  });

  // Prevent page dragging during the game.
  document.addEventListener("dragstart",e=>e.preventDefault());

  // Pause when app is hidden.
  document.addEventListener("visibilitychange",()=>{
    if(document.hidden && running && !paused) togglePause();
  });

  show("titleScreen");
})();
</script>
</body>
</html>

Just an interval player.

Use JS in browser console:

let V_Interval = 5;
let video = document.querySelector("video");
let lastStartTime = 0;
let pausedAtTime = 0;

function playInterval(startTime) {
    if (!video) return;

    video.currentTime = startTime;
    video.play();

    setTimeout(() => {
        video.pause();
        lastStartTime = startTime; // Save last interval start time
        pausedAtTime = video.currentTime; // Save exact pause position
    }, V_Interval * 1000);
}
document.addEventListener("keydown", (event) => {
    if (!video) return;

    if (event.key === "ArrowRight") {
        // Continue from where it paused
        playInterval(pausedAtTime);
    } else if (event.key === "ArrowLeft") {
        // Replay last interval
        playInterval(lastStartTime);
    }
});

playInterval(video.currentTime);

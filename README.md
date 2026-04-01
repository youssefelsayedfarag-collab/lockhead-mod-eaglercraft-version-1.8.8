let lockedYaw = null;
let lockedPitch = null;
let enabled = true;

document.addEventListener("keydown", (e) => {
    if (e.key === "l" || e.key === "L") {
        enabled = !enabled;
        console.log("LockHead: " + (enabled ? "ON" : "OFF"));
        lockedYaw = null;
        lockedPitch = null;
    }
});

function lockHead() {
    if (!enabled) return;

    let player = window.ModAPI && ModAPI.player;
    if (!player) return;

    if (lockedYaw === null) {
        lockedYaw = player.rotationYaw || 0;
        lockedPitch = player.rotationPitch || 0;
    }

    player.rotationYaw = lockedYaw;
    player.rotationPitch = lockedPitch;
}

setInterval(lockHead, 50);

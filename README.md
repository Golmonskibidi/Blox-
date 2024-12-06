const toilette = document.getElementById('toilette');
const ogre = document.getElementById('ogre');
const obstacle = document.getElementById('obstacle');
const gameOverScreen = document.getElementById('game-over');
const winScreen = document.getElementById('win');

let isGameOver = false;
let position = 10; // Position de la toilette

// Déplacement de la toilette avec les touches fléchées
document.addEventListener('keydown', (event) => {
    if (isGameOver) return;

    if (event.key === 'ArrowUp') {
        position = Math.max(0, position - 10);
        toilette.style.bottom = position + 'px';
    } else if (event.key === 'ArrowDown') {
        position = Math.min(window.innerHeight - 70, position + 10);
        toilette.style.bottom = position + 'px';
    }
});

// Détection de collision
function checkCollision() {
    const toiletteRect = toilette.getBoundingClientRect();
    const ogreRect = ogre.getBoundingClientRect();
    const obstacleRect = obstacle.getBoundingClientRect();

    // Collision avec l'ogre
    if (
        toiletteRect.right > ogreRect.left &&
        toiletteRect.left < ogreRect.right &&
        toiletteRect.bottom > ogreRect.top &&
        toiletteRect.top < ogreRect.bottom
    ) {
        isGameOver = true;
        gameOverScreen.classList.remove('hidden');
    }

    // Collision avec l'obstacle
    if (

# YxV
function startGame() {
    alert("Bienvenue dans le jeu de devinette de nombre!");

    let maxAttempts = getNumberOfAttempts();
    let targetNumber = generateRandomNumber();

    playGame(targetNumber, maxAttempts);
}

function getNumberOfAttempts() {
    let attempts;
    do {
        attempts = parseInt(prompt("Entrez le nombre de tentatives (entre 1 et 20) :"));
    } while (isNaN(attempts) || attempts < 1 || attempts > 20);

    return attempts;
}

function generateRandomNumber() {
    return Math.floor(Math.random() * 100) + 1;
}

function playGame(targetNumber, maxAttempts) {
    let attempts = 0;

    while (attempts < maxAttempts) {
        let guess = prompt(`Tentative ${attempts + 1} de ${maxAttempts}. Entrez un nombre :`);

        if (guess === null) {
            alert("Le jeu a été annulé.");
            return;
        }

        guess = parseInt(guess);

        if (isNaN(guess)) {
            alert("Ce n'est pas un nombre !");
        } else {
            if (guess === targetNumber) {
                alert(`Bravo ! Vous avez gagné en ${attempts + 1} tentatives.`);
                return;
            } else {
                let message = guess < targetNumber ? "trop petit" : "trop grand";
                alert(`Tentative ${attempts + 1} de ${maxAttempts} : ${guess} est ${message}.`);
            }
            attempts++;
        }
    }

    alert(`Vous avez utilisé toutes vos tentatives. Le nombre à trouver était ${targetNumber}. Vous avez perdu !`);
}

function askForReplay() {
    return confirm("Voulez-vous rejouer ?");
}

do {
    startGame();
} while (askForReplay());

alert("Merci d'avoir joué !");

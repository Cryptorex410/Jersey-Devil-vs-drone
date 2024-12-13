<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jersey Devil vs Drone</title>
    <script src="https://cdn.jsdelivr.net/npm/phaser@3.55.2/dist/phaser.min.js"></script>
    <style>
        body { margin: 0; overflow: hidden; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="game.js"></script>
</body>
</html>
// Define the game configuration
var config = {
    type: Phaser.AUTO,
    width: 800,
    height: 600,
    scene: {
        preload: preload,
        create: create,
        update: update
    }
};

var player1, player2;
var player1Health = 100;
var player2Health = 100;
var cursors;
var attacking = false;

// Create the game instance
var game = new Phaser.Game(config);

function preload() {
    // Load images for characters and backgrounds
    this.load.image('jerseyDevil', 'https://example.com/jersey_devil_image.png');  // Replace with actual URL
    this.load.image('drone', 'https://example.com/drone_image.png');  // Replace with actual URL
    this.load.image('background', 'https://example.com/background_image.png');  // Replace with actual URL
}

function create() {
    // Set up background
    this.add.image(400, 300, 'background');
    
    // Create player characters
    player1 = this.add.sprite(100, 500, 'jerseyDevil');
    player2 = this.add.sprite(700, 500, 'drone');
    
    // Set up text to show health
    var style = { font: '32px Arial', fill: '#fff' };
    this.add.text(20, 20, 'Jersey Devil Health: ' + player1Health, style);
    this.add.text(500, 20, 'Drone Health: ' + player2Health, style);

    // Add cursors for player movement
    cursors = this.input.keyboard.createCursorKeys();
    
    // Add controls for space to attack
    this.input.keyboard.on('keydown-SPACE', attack, this);
}

function update() {
    // Move player1 (Jersey Devil)
    if (cursors.left.isDown) {
        player1.x -= 5;
    }
    if (cursors.right.isDown) {
        player1.x += 5;
    }
    
    // Move player2 (Drone)
    if (cursors.up.isDown) {
        player2.x -= 5;
    }
    if (cursors.down.isDown) {
        player2.x += 5;
    }
    
    // Check for collision between players (for attack)
    if (Phaser.Geom.Intersects.RectangleToRectangle(player1.getBounds(), player2.getBounds()) && attacking) {
        player2Health -= 10;
        if (player2Health <= 0) {
            player2Health = 0;
            this.add.text(300, 250, 'Jersey Devil Wins!', { font: '40px Arial', fill: '#ff0000' });
        }
        attacking = false;
    }
    
    // Display health
    this.children.getByName('healthText1').setText('Jersey Devil Health: ' + player1Health);
    this.children.getByName('healthText2').setText('Drone Health: ' + player2Health);
}

function attack() {
    attacking = true;
}

# bernoso
let trator;
let plantas = [];

function setup() {
  createCanvas(1000, 500);
  trator = new Trator(0, 400);

  // Criar linha de plantas
  for (let x = 0; x < width; x += 50) {
    plantas.push(new Planta(x + 10, 390));
  }
}

function draw() {
  background(100, 200, 100); // Campo verde
  desenharCampo();

  // Mostrar e colher as plantas
  for (let i = 0; i < plantas.length; i++) {
    if (!plantas[i].colhida) {
      plantas[i].mostrar();

      // Verifica colisão com o trator
      if (trator.x + 120 > plantas[i].x && trator.x < plantas[i].x + 20) {
        plantas[i].colhida = true;
      }
    }
  }

  trator.mostrar();
  trator.mover();
}

// Classe Trator
class Trator {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.velocidade = 2;
  }

  mover() {
    this.x += this.velocidade;
    if (this.x > width) {
      this.x = -120;
    }
  }

  mostrar() {
    // Corpo do trator
    fill(255, 0, 0);
    rect(this.x, this.y - 60, 120, 60);

    // Cabine
    fill(0, 0, 255);
    rect(this.x + 20, this.y - 100, 50, 40);

    // Rodas
    fill(50);
    ellipse(this.x + 20, this.y, 40, 40);
    ellipse(this.x + 100, this.y, 40, 40);
  }
}

// Classe Planta com formato melhorado
class Planta {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.colhida = false;
  }

  mostrar() {
    // Haste marrom
    fill(139, 69, 19);
    rect(this.x + 5, this.y - 20, 5, 20);

    // Folhas verdes (duas elipses em forma de V)
    fill(0, 150, 0);
    ellipse(this.x, this.y - 20, 15, 30);  // Esquerda
    ellipse(this.x + 15, this.y - 20, 15, 30); // Direita
  }
}

// Linhas do campo
function desenharCampo() {
  stroke(80, 160, 80);
  for (let i = 0; i < width; i += 50) {
    line(i, 0, i, height);
  }
}

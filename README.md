# IA TOURNAMENT BOT

<div align="center">
  <h1>This repository has been created to develop my bot</h1>
</div>

<div>

  <h3>1. Reglas del Juego</h3>
  <ul>
    <li>El juego se juega en una cuadrícula de 9 columnas y 7 filas.</li>
    <li>El Jugador 1 utiliza X y el Jugador 2 utiliza O para marcar sus movimientos.</li>
    <li>Los jugadores se turnan para dejar caer una ficha en una de las columnas.</li>
    <li>La ficha cae hasta la posición más baja disponible en la columna seleccionada.</li>
    <li>Un jugador gana si conecta cinco de sus fichas en una fila, columna o diagonal.</li>
    <li>Si la cuadrícula se llena completamente sin un ganador, el juego termina en empate.</li>
  </ul>

  <p>⚠️ <span style="font-weight: bold">Columnas especiales:</span> El tablero ha sido modificado para incluir columnas especiales que pueden cambiar completamente el resultado del juego. En cada enfrentamiento se seleccionarán aleatoriamente 2 columnas con un efecto especial. Cuando una ficha cae en una de estas columnas pueden ocurrir tres cosas:</p>
  <ul>
    <li>Con una probabilidad p la ficha se moverá a la columna de la izquierda.</li>
    <li>Con una probabilidad q la ficha se moverá a la columna derecha.</li>
    <li>Con una probabilidad 1 - p - q la ficha caerá en la misma posición en que se dejó caer.</li>
  </ul>

  <p>💡 <span style="font-weight: bold">Consejo:</span> Asegúrate de que tu bot pueda manejar estas columnas especiales. Se mantendrá en secreto el valor de p y q para cada enfrentamiento pero siempre serán las mismas columnas y valores para todas las partidas de un mismo enfrentamiento.</p>

  <h3>2. Requisitos para los Bots</h3>
  <p>Cada participante debe presentar una clase en Python que implemente su bot. La clase debe cumplir con los siguientes requisitos:</p>

  <p style="font-weight: bold">Estructura de la Clase</p>

  <ul>
    <li>El nombre de la clase será el nombre de tu bot.</li>
    <li>La clase del bot debe definir un método llamado <code>get_move</code>.</li>
    <ul>
      <li>
        <span style="font-weight: bold">Signature del Método:</span>
      </li>
    </ul>
  </ul>
  <div align="center">
    <code>def get_move(self, board: list[list[int]], player: int, T: int, N: int) -> int:</code>
  </div>
  <ul>
    <ul>
      <li>
        <span style="font-weight: bold">Parámetros:</span>
      </li>
      <ul>
        <li>
          <code>board</code>
          : Una lista 2D que representa el estado del juego. Cada elemento puede ser:
        </li>
        <ul>
          <li>
            <code>0</code>
            : Una celda vacía.
          </li>
          <li>
            <code>1</code>
            : Una celda ocupada por el Jugador 1.
          </li>
          <li>
            <code>2</code>
            : Una celda ocupada por el Jugador 2.
          </li>
        </ul>
        <li>
          <code>player</code>
          : Un entero (1 o 2) que indica el jugador actual.
        </li>
        <li>
          <code>T</code>
          : Un entero que representa el tiempo máximo disponible para realizar un movimiento (en segundos).
        </li>
        <li>
          <code>N</code>
          : Un entero que representa el número total de partidas realizados hasta ahora contra el mismo oponente.
        </li>
      </ul>
      <li>
        <span style="font-weight: bold">Output:</span>
      </li>
      <ul>
        <li>
          Un entero que representa la columna donde el bot quiere colocar su ficha.
        </li>
      </ul>
    </ul>
    <li>
      El bot debe implementar adicionalmente un método <code>train</code> que no recibe parámetros y no retorna nada. Este método se llamará una vez después de cada enfrentamiento y puede ser utilizado para entrenar el bot.
    </li>
    <li>
      Por último, el bot puede implementar un método <code>adjust</code> que no recibe parámetros y no retorna nada. Este método se llamará una vez al final de cada PARTIDA y puede ser utilizado para ajustar pesos o hiperparámetros del bot durante el enfrentamiento.
    </li> 
  </ul>

  <h3>Entorno del bot</h3>
    <ul>
      <li>
        El bot tendrá acceso a una carpeta llamada `data` en la misma ubicación que el archivo de tu bot. Esta carpeta contendrá los pesos de un modelo pre-entrenado o cualquier otro archivo que quieras que tu bot utilice.
      </li>
      <li>
        El bot tendrá acceso a una carpeta llamada `logs` en la misma ubicación que el archivo de tu bot. Esta carpeta contendrá los logs de los enfrentamientos. Los logs contendrán información sobre el estado del tablero después de cada movimiento y el resultado de cada partida. Los logs vendrán en formato JSON.
      </li>
    </ul>

  ```
  bot_folder/
  │
  ├── bot.py
  │
  ├── data/
  │   ├── model_weights.h5
  │   ├── ...
  │
  └── logs/
      ├── log_1.json
      ├── ...
  ```
  <span style="font-weight: bold">Ejemplo de Implementación</span>
  <p>Aquí tienes un ejemplo simple de un bot válido:</p>

  ```
  class RandomBot:
      import random

      def get_move(self, board, player, T, N):
          valid_moves = [col for col in range(len(board[0])) if board[0][col] == 0] # Consejo: esto debería estar siempre
          return self.random.choice(valid_moves)

      def train(self):
          pass # Puedes entrenar tu bot aquí si lo deseas

      def adjust(self):
          pass # Puedes ajustar tu bot aquí si lo deseas
  ```


  <h3>3. Reglas de Presentación</h3>
  <ul>
    <li>
      Los bots no deben intentar modificar el tablero directamente ni realizar movimientos ilegales.
    </li>
    <li>
      Si un bot intenta un movimiento inválido (por ejemplo, seleccionar una columna llena o fuera de los límites), perderá el juego.
    </li>
    <li>
      Tu bot no debe exceder un límite de tiempo 
      <span style="font-weight: bold">T</span> por movimiento.
    </li>
  </ul>

  <h3>4. Formato del Torneo</h3>
  <p style="font-weight: bold">Todos contra todos</p>
  <p>Se presenta un formato de liga, donde cada bot se enfrentará contra todos los demás bots a modalidad de ida y vuelta.</p>


  <ul>
    <li>
      Cada enfrentamiento consistirá de dos fases:
    </li>
    <ul>
      <li>
        <span style="font-weight: bold">Fase 1</span>
          : Un máximo de 99 partidas con movimientos de 1 segundo cada uno. Ganará el bot que gane antes 50 partidas.
      </li>
      <li>
        <span style="font-weight: bold">Fase 2</span>
          : Un máximo de 9 partidas con movimientos de 10 segundos cada uno. Ganará el bot que gane antes 5 partidas.
      </li>
    </ul>
    <li>
      Se otorgarán puntos en cada fase de la siguiente manera:
    </li>
    <ul>
      <li>
        <span style="font-weight: bold">Victoria</span>
          : 1 puntos.
      </li>
      <li>
        <span style="font-weight: bold">Derrota</span>
          : -1 puntos.
      </li>
    </ul>
    <li>
      El bot con la mayor puntuación total al final del torneo será el ganador.
    </li>
  </ul>


  <h3>5. Presentación de tu Bot</h3>
  <ul>
    <li>
      Envía tu bot como un archivo .zip con el nombre de la clase coincidiendo con el nombre de tu bot.
    </li>
  </ul>

  ```
  <Tu nombre>.zip
  |
  ├── <Nombre de tu bot>.py
  └── data/
      ├── model_weights.h5
      ├── ...
  ```

  <ul>
    <li>
      Envía tu bot por correo electrónico a <a href="https://github.com/carlospov" target="_blank">Carlos Poveda</a>  antes del 26 de abril.
    </li>
  </ul>

  <h3>6. Notas Importantes</h3>
  <ul>
    <li>
      Los bots que generen errores en tiempo de ejecución durante un enfrentamiento perderán ese enfrentamiento.
    </li>
    <li>
      Las decisiones del juez son definitivas.
    </li>
  </ul>
</div>

---
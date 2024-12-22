html y PHP
``` bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora</title>
    <link rel="stylesheet" href="calculadora.css">
</head>
<body>
    <div class="calculator">
        <h1>Calculadora</h1>
        <form method="POST" action="">
            <label for="num1">Número 1:</label>
            <input type="number" id="num1" name="num1" step="any" required>

            <label for="num2">Número 2 (opcional para raíz):</label>
            <input type="number" id="num2" name="num2" step="any">

            <label for="operacion">Operación:</label>
            <select name="operacion" id="operacion" required>
                <option value="suma">Suma</option>
                <option value="resta">Resta</option>
                <option value="multiplicacion">Multiplicación</option>
                <option value="division">División</option>
                <option value="raiz">Raíz cuadrada (solo utiliza el primer número)</option>
            </select>

            <button type="submit" name="submit">Calcular</button>
        </form>
    </div>
    <?php
    if (isset($_POST["submit"])) {
        $num1 = isset($_POST["num1"]) ? (float)$_POST["num1"] : 0;
        $num2 = isset($_POST["num2"]) ? (float)$_POST["num2"] : 0;
        $operacion = $_POST["operacion"];
        $resultado = null;
        $resultado2 = null;

        switch ($operacion) {
            case 'suma':
                $resultado = $num1 + $num2;
                break;
            case 'resta':
                $resultado = $num1 - $num2;
                break;
            case 'multiplicacion':
                $resultado = $num1 * $num2;
                break;
            case 'division':
                if ($num2 !=0) {
                    $resultado = round($num1 / $num2,2);
                } else{
                    $resultado = "Use otro numero que no sea cero";
                }
                break;
            case 'raiz':
                if ($num1 >= 0 && $num2 >= 0) {
                    $resultado = "La raíz cuadrada de $num1 es ".round(sqrt($num1),2);
                    $resultado2 = " y la raíz cuadrada de $num2 es ".round(sqrt($num2),2);
                    $resultado .= $resultado2;
                } elseif ($num1 < 0 && $num2 < 0) {
                    $resultado = "Error: No se puede calcular la raíz cuadrada de números negativos ($num1 y $num2).";
                } elseif ($num1 < 0) {
                    $resultado = "Error: No se puede calcular la raíz cuadrada de $num1 porque es negativo.";
                } else {
                    $resultado = "Error: No se puede calcular la raíz cuadrada de $num2 porque es negativo.";
                }
                break;
            
            default:
                $resultado = "Operación no válida.";
                break;
        }

            echo "<div class='result'><strong>Resultado:</strong> $resultado</div>";
        }
        ?>
    </div>
</body>
</html>

```

CSS:

``` bash
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f9;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.calculator {
    background: #fff;
    border-radius: 10px;
    box-shadow: 0 4px 8px #0000001a;
    padding: 30px;
    width: 320px;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.calculator h1 {
    font-size: 24px;
    margin-bottom: 20px;
    color: #333;
}


.calculator form {
    display: grid;
    gap: 15px;
    text-align: left;
}

.calculator label {
    font-weight: bold;
    font-size: 14px;
    color: #555;
}


.calculator input,
.calculator select {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
}


.calculator button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 12px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.calculator button:hover {
    background-color: #0056b3;
}


.result {
    margin-top: 20px;
    font-size: 18px;
    font-weight: bold;
    color: #007bff;
    text-align: center;
    padding: 15px;
    border: 1px solid #007bff;
    border-radius: 5px;
    background: #f0f8ff;
}


@media (max-width: 480px) {
    .calculator {
        width: 90%;
        padding: 20px;
    }

    .calculator h1 {
        font-size: 20px;
    }

    .calculator label {
        font-size: 12px;
    }

    .calculator button {
        padding: 10px;
    }
}

```

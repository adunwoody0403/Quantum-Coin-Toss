# Quantum Coin Toss

<p>A basic and experimental introduction to quantum computing. This program serves to simulate a fair coin toss by utilizing the quantum superposition of a single qubit in order to determine a random result with 50% probability of each outcome.</p>

<p>This is a python program and makes use of the Qiskit library in order to execute quantum operations. Using Qiskit we are able to run the quantum operations on both simulated hardware, as well as real hardware available within the IBM Quantum platform.</p>

<p>This program can be run on the cloud via IBM Quantum Lab using the provided Jupyter notebook. It can also be run locally by installing Python and Qiskit. To run locally you will need an IBM Quantum account. <a href="https://qiskit.org/documentation/getting_started.html">Click here for a more detailed guide.</a></p>

## Running On Simulated Hardware
Here is the code to simulate a coin toss using a single qubit. By executing this code as is, we can simulate a single-qubit quantum circuit locally without the need for real quantum hardware. This program will result in a single output and will report a win or a loss depending on the player's choice.
```python
from qiskit import *
from qiskit.providers.aer import QasmSimulator

playerChoice = 0 # Heads
#playerChoice = 1 # Tails

backend = QasmSimulator()

# Setup quantum circuit.
circuit = QuantumCircuit(1, 1)
circuit.h(0)
circuit.measure([0], [0])
compiledCircuit = transpile(circuit, backend)

# Execute circuit.
job = backend.run(compiledCircuit, shots=1)

# Process results.
result = job.result()
counts = result.get_counts(compiledCircuit)

# Print result.
if '0' in counts.keys():
    # Measurement is heads.
    if playerChoice == 0: print("Heads. You win.")
    else: print ("Heads. You lose.")

else:
    # Measurement is tails.
    if playerChoice == 0: print ("Tails. You lose.")
    else: print ("Tails. You win.")
 
```
## Quantum Circuit
The resulting quantum circuit of the above program is very simple. We can view a visual representation of the circuit with the following command
```Python
# Draw circuit
circuit.draw()
```

![QuantumCircuit](Images/QuantumCoinTossCircuit.PNG)

As we can see from the image, our circuit consists of two parts. First we define a qubit (q). We then execute a quantum operation to put the qubit into a quantum superposition state, this is denoted by H. After putting the qubit into the superposition state, we observe its value and write the value into a constant (C). Now that the qubit value has been observed, it is no longer in a superposition state and its value will remain constant. Its value will determine whether our coin toss landed on heads or tails.

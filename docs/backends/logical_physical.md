# Logical mode and physical mode

Since the purpose of cat qubits is to create logical qubits with a very low error rate, a processor based on cat qubits can run in two modes: physical and logical.

### Physical mode

In the physical mode, you’re working directly with cat qubits: one qubit in your quantum circuit corresponds to one physical cat qubit on the chip.

This enables you to leverage the biased noise of cat qubits for your error correction experiments, but only lets you use a limited set of gates (see [Supported instructions](../reference/supported_instructions.md) for more details).

Indeed, when using cat qubits in physical mode, it only makes sense to use so-called “bias-preserving” gates, which do no leak information from the noisy phase channel to the clean bit channel.

This means that gates such as the Hadamard gate are forbidden, since they do contaminate the bit channel with phase errors.

In physical mode, you’ll also need to take the chip’s connectivity into account, since cat qubits are usually only connected with their nearest neighbor. Although Qiskit’s transpiler can do this job for you, transpilation may push the qubit number beyond the limits of what the emulator or the chip can do.

You’ll use the physical mode if you want to study the **properties of cat qubits**, implement **error correction** or create your own **logical qubit**.

### Logical mode

In the logical mode, you’re working with error-corrected logical qubits: one qubit in your quantum circuit corresponds to a group of several physical qubits on the chip.

This mode is more abstract that the physical mode, since all the error correction operations leveraging several physical qubits are hidden in the compilation step.

But **the logical mode is the perfect choice to run quantum algorithms**: you can execute any quantum gate, you get low error rates and all-to-all connectivity.

Also, the logical mode does not feature a noise bias as strong as in physical mode. The exact bias depends on the tuning of the chip (distance of the code, number of photons), but a good tuning can make bit-flip and phase-flip errors equally (un)likely.

The logical mode is only possible with chips featuring enough physical cat qubits to run an effective error correction code. We estimate this minimal number to be somewhere between 5 (for a first demonstration of a single logical qubit) and 40 (for very high fidelities or multi-qubit logical operations).
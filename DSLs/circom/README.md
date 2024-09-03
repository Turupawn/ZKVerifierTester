## Generate Verifier

```bash
circom multiplier2.circom --r1cs --wasm --sym --c
snarkjs powersoftau new bn128 12 pot12_0000.ptau -v
echo 123 | snarkjs powersoftau contribute pot12_0000.ptau pot12_0001.ptau --name="First contribution" -v
snarkjs powersoftau prepare phase2 pot12_0001.ptau pot12_final.ptau -v
snarkjs groth16 setup multiplier2.r1cs pot12_final.ptau multiplier2_0000.zkey
echo 321 | snarkjs zkey contribute multiplier2_0000.zkey multiplier2_0001.zkey --name="1st Contributor Name" -v
snarkjs zkey export solidityverifier multiplier2_0001.zkey verifier.sol
```

The Groth16 verifier is now located at `verifier.sol`.
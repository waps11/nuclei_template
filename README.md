# Nuclei Template - Post-Quantum Cryptographic Algorithm Detection

## Description
This Nuclei template detects and extracts post-quantum cryptographic (PQC) algorithms supported by **TLS 1.3** servers.

## Detected Algorithms

### Key Encapsulation Mechanisms (KEM)
- **Kyber** (512, 768, 1024) - NIST standardized algorithm
- **NTRU** - Robust alternative
- **Classic McEliece** - Based on error-correcting codes
- **SABER** - Algorithm based on Euclidean lattices

### Digital Signatures
- **Dilithium** (2, 3, 5) - NIST standardized
- **Falcon** (512, 1024) - Compact signatures
- **SPHINCS+** - Hash-based

### Hybrid Schemes
- X25519_Kyber768
- P256_Kyber512
- P384_Kyber768
- ECDHE_KYBER

## Installation

Make sure you have Nuclei installed:
```bash
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## Usage

### Scan a single server
```bash
nuclei -t pqc-detector.yaml -u https://example.com
```

### Scan a list of servers
```bash
nuclei -t pqc-detector.yaml -l servers.txt
```

### Scan with a custom port
```bash
nuclei -t pqc-detector.yaml -u https://example.com:8443
```

### Scan with verbosity
```bash
nuclei -t pqc-detector.yaml -l servers.txt -v
```

### Export results to JSON
```bash
nuclei -t pqc-detector.yaml -l servers.txt -json -o results.json
```

### Export results to Markdown
```bash
nuclei -t pqc-detector.yaml -l servers.txt -markdown-export results.md
```

## Server List File Format

Create a `servers.txt` file with one URL per line:
```
https://server1.example.com
https://server2.example.com:8443
https://server3.example.com:443
```

## Example Output

```
[pqc-detector] [ssl] [info] https://example.com:443
  [pqc_algorithms] X25519Kyber768
  [tls_version] TLSv1.3
```

## Results Interpretation

- **INFO**: The server supports post-quantum cryptographic algorithms
- Extractors display:
  - `pqc_algorithms`: Detected PQC algorithms
  - `tls_version`: TLS protocol version
  - Complete cipher information with algorithm details

## Important Notes

1. **TLS 1.3 Only**: This template only scans TLS 1.3 connections
2. **Limited current support**: Most production servers do not yet support PQC
3. **Experimental implementations**: Some servers may have test implementations
4. **Evolving standards**: Algorithm names may vary by implementation (legacy names like "Kyber" vs standardized "ML-KEM")
5. **Performance**: PQC algorithms may be slower than classical algorithms

## References

- [NIST Post-Quantum Cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography)
- [Open Quantum Safe Project](https://openquantumsafe.org/)
- [Cloudflare PQC](https://blog.cloudflare.com/post-quantum-for-all/)

## License

This template is licensed under the GNU General Public License v3.0 (GPL-3.0).

See the [LICENSE](LICENSE) file for details or visit https://www.gnu.org/licenses/gpl-3.0.en.html

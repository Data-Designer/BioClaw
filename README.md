# BioClaw 🧬

**Your AI biology research assistant on WhatsApp.** Run BLAST searches, analyze sequences, process genomic data — all from your phone.

Built on [NanoClaw](https://github.com/qwibitai/nanoclaw) + Claude Agent SDK. Agents run in isolated containers pre-loaded with bioinformatics tools.

## What It Does

Message `@Bio` on WhatsApp and it can:

```
@Bio BLAST this sequence against nr: ATGCGATCGATCG...
@Bio analyze the FastQC report in my workspace
@Bio find all ORFs in sequence.fasta and annotate them
@Bio run differential expression analysis on counts.csv
@Bio search PubMed for recent papers on CRISPR delivery methods
@Bio align these reads to the human reference genome
@Bio visualize the gene expression heatmap from my RNA-seq data
@Bio what's the 3D structure of protein P53? fetch from PDB
```

## Biology Tools in Container

### Command-Line
| Tool | What it does |
|------|-------------|
| **BLAST+** | Sequence similarity search (blastn, blastp, blastx, tblastn) |
| **SAMtools** | SAM/BAM manipulation, sorting, indexing |
| **BEDTools** | Genome arithmetic, interval operations |
| **BWA** | Short-read alignment to reference genomes |
| **minimap2** | Long-read and assembly alignment |
| **FastQC** | Sequencing data quality control |
| **seqtk** | FASTA/FASTQ toolkit |

### Python Libraries
| Library | What it does |
|---------|-------------|
| **BioPython** | Sequence I/O, NCBI Entrez, phylogenetics, PDB |
| **pandas / NumPy / SciPy** | Data analysis and statistics |
| **matplotlib / seaborn** | Publication-quality plots |
| **scikit-learn** | Machine learning on biological data |
| **RDKit** | Cheminformatics, molecular structures |
| **PyDESeq2** | Differential gene expression analysis |
| **scanpy** | Single-cell RNA-seq analysis |
| **pysam** | Python interface to SAMtools |

## Quick Start

```bash
git clone https://github.com/YOUR_USERNAME/BioClaw.git
cd BioClaw
claude
```

Then run `/setup`. Claude Code handles everything: dependencies, WhatsApp auth, container build with bio tools.

## How It Works

```
WhatsApp (@Bio) --> SQLite --> Polling loop --> Container (Claude + Bio Tools) --> Response
```

Single Node.js process. Each group gets its own isolated container with biology tools pre-installed. Per-group memory and file storage.

## Configuration

Default trigger word is `@Bio`. Change it:
```
export ASSISTANT_NAME=MyLabBot
```

### Group Examples

- **Lab Group**: Mount your lab's shared sequencing data directory
- **Journal Club**: Schedule weekly PubMed searches for new papers
- **Personal**: Private analysis workspace with full project access

## Project Structure

```
BioClaw/
├── src/                    # Node.js orchestrator
│   ├── index.ts           # Main loop
│   ├── channels/whatsapp.ts
│   ├── container-runner.ts
│   └── ...
├── container/
│   ├── Dockerfile         # Agent image with bio tools
│   ├── build.sh
│   └── agent-runner/      # Claude Agent SDK runner
├── groups/
│   ├── main/CLAUDE.md     # Main channel memory
│   └── global/CLAUDE.md   # Shared memory
└── docs/
```

## Requirements

- macOS or Linux
- Node.js 20+
- Claude Code (`npm install -g @anthropic-ai/claude-code`)
- Apple Container (macOS) or Docker

## Customizing

Tell Claude Code what you want:

- "Add support for AlphaFold structure prediction"
- "Mount my lab's NAS at /workspace/data"
- "Schedule a daily PubMed alert for 'single-cell spatial transcriptomics'"
- "Add Telegram support instead of WhatsApp"

The codebase is small enough that Claude can safely modify it.

## Acknowledgments

Inspired by and built on [NanoClaw](https://github.com/qwibitai/nanoclaw) by [@qwibitai](https://github.com/qwibitai). MIT License.

## License

MIT

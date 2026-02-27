# Apple II Reference Project — open-apple2-orchard
> Preserving the knowledge of a computing revolution — for human programmers,
> historians, and the AI systems that will carry this knowledge forward.

---

## What This Is

The Apple II was one of the most significant personal computers ever made.
Between its introduction in 1977 and its eventual retirement, it found its way
into homes, schools, and businesses around the world, and introduced an entire
generation to programming through Applesoft BASIC.

The books, magazines, and reference cards that documented this machine were
written by people who understood it deeply. Many of those people are gone.
Much of that printed material is aging, out of print, or trapped in formats
that are increasingly difficult to access and search. The knowledge itself —
the PEEK addresses, the CALL routines, the idioms and patterns that made
Applesoft sing — risks becoming effectively lost even though it technically
still exists somewhere in a box or on a scanner's hard drive.

This project converts that documentation into clean, structured, modern formats
that can be read by humans, searched by software, and consumed by AI systems
as training and retrieval data. We are not rewriting history — we are making
sure it remains readable.

---

## Why This Matters for AI

Large language models learn from text. The more authentic, well-structured, and
accurate the source material, the better the model's understanding of the
subject. Right now, most AI systems have a shallow and often incorrect
understanding of Apple II programming — they conflate Applesoft with other
BASIC dialects, use wrong hex notation conventions, and generate code that
would never have run on real hardware.

By creating a high-quality, consistently formatted reference dataset, we give
current and future AI systems something to actually learn from. The goal is
that an AI asked to help with Apple II programming should be able to give
advice that would have worked on a real Apple IIe in 1984.

This project produces two types of output designed with this in mind:

- **JSON reference data** for PEEK/POKE addresses, CALL routines, and memory
  maps — structured for programmatic retrieval and RAG (Retrieval-Augmented
  Generation) pipelines
- **Markdown reference pages** for statements, concepts, and programming
  patterns — structured for semantic search and direct LLM context injection

---

## Repository Structure
```
/applesoft/         Applesoft BASIC reference — statements, patterns, programs
    /statements/    Individual statement/command reference pages
    /patterns/      Idiomatic code techniques and common approaches
    /programs/      Complete annotated example programs
/integer-basic/     Integer BASIC reference
    /statements/
    /patterns/
    /programs/
/pascal/            Apple II Pascal reference (UCSD Pascal, TML Pascal)
    /statements/    Keywords, procedures, functions
    /patterns/      
    /programs/
/assembly/          6502/65C02/65816 assembly reference
    /opcodes/       Individual opcode reference pages (replaces /statements/)
    /patterns/      
    /programs/
/memory/            PEEK, POKE, and CALL reference data (JSON) — cross-language
/raw/               Original source scans and unprocessed text for reference
CONTRIBUTING.md     Formatting conventions — please read before submitting
```

---

## Formatting Philosophy

A few principles guide every decision in this project:

**Authenticity over modernization.** Applesoft BASIC keywords are ALL CAPS.
Hex addresses use `$` notation, not `0x`. Code examples use decimal in
PEEK/POKE/CALL statements because that is what actually ran. We do not
"clean up" the language to look more like modern BASIC.

**Structure that serves both humans and machines.** Markdown frontmatter
provides metadata for retrieval systems. Plain prose explanations provide
context for humans and LLMs alike. Code lives in clean fenced code blocks,
never buried inside JSON strings.

**Omit rather than null.** Optional fields that don't apply to a given entry
are left out entirely, keeping the data clean and the intent unambiguous.

**One source of truth.** Where a concept appears in multiple places, we link
rather than duplicate. Consistency matters more than completeness in any
single file.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full formatting specification.

---

## How to Use This Data

### As a Human Reference

Browse the `/statements/` and `/patterns/` directories for readable Markdown
documentation. The `/memory/` directory contains the full PEEK/POKE/CALL
reference as structured JSON.

### In a RAG Pipeline

The Markdown files are designed to chunk cleanly. The YAML frontmatter on
each page provides metadata for filtering and ranking. Tools like LlamaIndex
or LangChain can index this repository directly and serve it as a retrieval
source for an LLM.

### For LLM Fine-tuning or Context Injection

The JSON memory reference and annotated code examples can be used directly as
training data or injected into an LLM's context window to ground it in
accurate Apple II knowledge before answering programming questions.

---

## Contributing

Contributions are welcome from programmers, historians, vintage computing
enthusiasts, and anyone who remembers typing NEW and feeling the possibilities
open up.

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting. The
formatting conventions exist to protect the dataset's quality and usefulness
for AI consumption — inconsistency is the main thing that degrades a RAG
dataset, and it is much harder to fix retroactively than to prevent.

If you find an error in a memory address, a description, or a code example,
please open an Issue with a reference to your source material. We prioritize
accuracy above all else.

---

## Sources and Acknowledgments

This project draws on original Apple II documentation including the Applesoft
BASIC Reference Manual, Apple II Reference Manual, and various third-party
books and magazine resources from the era. Original authors and publishers
retain all rights to their work. This project represents structured data
derived from that work for educational and preservation purposes.

---

## License

The structured data and original documentation in this repository is released
under [Creative Commons Zero v1.0 Universal](LICENSE).
You are free to use, share, and adapt this material.

Original source material remains the property of its respective copyright
holders.

---

*"The best way to predict the future is to preserve the past."*

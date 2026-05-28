# Building a Conifer Trait Matrix Using Large Language Models

<p align="center">
  <img src="https://github.com/madaime2/Conifer-Trait-Extractor/blob/main/Figures_LLM_Conifer_Project/PCA_Conifer_LLM.png/" width="750" title="hover text">
</p>

# Conifer Trait Matrix

LLM-assisted pipeline that builds a structured trait matrix for all conifer
species by extracting data from the Gymnosperm Database (conifers.org) and
augmenting it with the Kew Plant C-values Database, the IUCN Red List, and
World Flora Online.

## What it does

The pipeline scrapes every species page on conifers.org, uses an LLM to
extract morphological, ecological, reproductive, and genomic traits from the
text, verifies every extracted value against a verbatim quote from the source,
and combines the result with deterministic data from three external sources:

- **Kew Plant C-values Database** : genome size and ploidy
- **IUCN Red List API** : conservation status
- **World Flora Online** : accepted name and taxonomic status

Outputs three CSV files:

| Dataset | Contents |
|---|---|
| `dataset_A_text_evidenced.csv` | Only values extracted from the source text |
| `dataset_B_augmented.csv` | Dataset A plus Kew, IUCN, and family/genus rules |
| `dataset_C_sourced.csv` | Dataset B with a column indicating each value's source |

Plus a JSONL file with the original evidence reported for every extracted value.

## Requirements

- Python 3.9+
- An OpenAI API key
- (Optional) An IUCN Red List API token for conservation status
- The packages listed in `requirements.txt`

To run locally:

```bash
pip install -r requirements.txt
export OPENAI_API_KEY="Add-Here"
python conifers_extractor.py
```

## Trait coverage

Forty-one traits across six categories: morphology, reproduction, leaves,
seeds and cones, cytogenetics, ecology, and conservation. Coverage is uneven:
morphological traits are well populated, ecological traits are sparser, and
genome size / ploidy depend on what is available in Kew C-values.

## Caveats

- Trait accuracy depends on the conifers.org pages; outdated descriptions
  propagate into the matrix.
- The LLM can hallucinate. Evidence verification catches most cases but not
  all.
- Taxonomic status reflects World Flora Online and may differ from other
  authorities.

## Citation

If you use this method, please cite:

> Adaime, M.-E. (2026). Conifer Trait Matrix [Software]. Smithsonian
> Institution Data Science Lab.
> https://github.com/madaime2

## Contact

Marc-Élie Adaime, Chief Data and AI Office, Office of Digital and Innovation, Smithsonian Institution

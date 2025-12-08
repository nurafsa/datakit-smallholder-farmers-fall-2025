# cnmetzi - Financial Inclusion Analysis

## Overview
Goal: Explore how smallholder farmers discuss financial topics such as market prices, credit access, savings, and other non-farming livelihood concerns to better understand their economic realities and opportunities for inclusion.

## Research Questions
- Question 1: How can we identify financial-related questions?
- Question 2: What patterns do we see in financial-related questions?

## Methodology

### Data Sources
- Using Producers Direct dataset 

### Approach
1. **Step 1**: Data loading and initial exploration
2. **Step 2**: Data cleaning and preprocessing, 
extracted only Eng tagged questions
Used this as starting financial word list: investment, loan, grant, interest, rate, insurance, credit, subsidy, lease, price, agri-loan, microfinance, cost, income, bank, finance, futures, refinance, mortgage, supply, financing, contract, guarantee, compensation, capital, payment, invest, revenue, MSP, borrow, lend, audit, equity, balance, cash flow, fund, funding, budget, liability, asset, invoice, payment, pay, tax, expense, loss, profit, debt, cooperative, market, sell, buy, yield, money, order, sale, profit, capit, cash
3. **Step 3**: Analysis techniques applied
4. **Step 4**: Visualization and interpretation
5. **Step 5**: Validation and testing

### Tools and Technologies
- **Programming Language**: Python 3.11.14
- **Key Libraries**: pandas, numpy, matplotlib, seaborn, nltk, collections, regex  
- **GenAI Tools Used**: ChatGPT
- **Other Tools**: Jupyter Notebook

## Use of Generative AI

### Tools Used
- **ChatGPT**: Used for generating list of possibly farming finance related keywords and generating a subset list of likely finance related stems from all English question stems

### Human Review Process
- All AI-generated code was reviewed and tested for accuracy
- AI-generated insights were validated against the data


### AI-Assisted vs. Human-Created
- **AI-Assisted**: Generate initial possible farming finance related keywords and reduce existing stems to those possibly related to finance; writing functions quickly for stemming and counting
- **Human-Created**: [List which parts, e.g., "All analysis logic, interpretation, and conclusions"]

## Key Findings

### Finding 1: Big gap in question topic data availability
Roughly 25% of the English tagged questions do not have a topic, and there are no topics that align to Finance

**Implications for Producers Direct:**
- Given the significant gap in topic data treat analysis done on available topics with caution knowing that there are many questions not tagged with topic 
- Recommend using the question content for topic analysis especially for financial topics

### Finding 2: [Title]
Description of the finding, supported by data and visualizations.

**Implications for Producers Direct:**
- How this finding can be used
- What actions it suggests

### Finding 3: [Title]
Description of the finding, supported by data and visualizations.

**Implications for Producers Direct:**
- How this finding can be used
- What actions it suggests

## Visualizations

### [Visualization 1 Title]
![Visualization 1](visualizations/viz1.png)

**Interpretation**: What this visualization shows and why it matters.

### [Visualization 2 Title]
![Visualization 2](visualizations/viz2.png)

**Interpretation**: What this visualization shows and why it matters.

## Limitations and Challenges

### Data Limitations
- There needs to be a technique developed to treat question repeated by different users on the same day which probably all stem from trying to answer the original question vs everyone asking it independently 

### Methodological Limitations
- Limited EDA was done that would potentially show the need for more data cleansing or preparation
- Assumed questions tagged as eng would basically be in English, each question has a unqiue id without error or duplicates due to time contrainst (this should be checked)
- Simplified by just looking at questions versus the question and answer both to see if the discussion was related to Finance
- If we had some question data that was labeled as Financial or not that would be helpful to use with other modeling or checking how well the keyword approach picks up relevant questions

### Technical Challenges
- Computational constraints
- Translation accuracy issues
- Other technical hurdles

### Miscellaneous
- When looking at common stems I noticed some words from other languages were still used in the english questions and should potentially be translated when doing other topic analysis, i.e. obuyambi (sometimes mispelled obuyabi), buyinza
- Also words are sometimes mispelled so when doing keyword analysis I found it useful to start with all the words used and then select Finance related ones to capture spelling variations

## Next Steps and Recommendations

### For Further Analysis
1. **Recommendation 1**: Need to do more work to figure out how to reduce or better understand when the same question is repeated by different users and question ids on the same day but seems to all be from the same original question
2. **Recommendation 2**: How to deepen this analysis
3. **Recommendation 3**: Related questions to investigate

### For Producers Direct
1. **Action 1**: Specific recommendation for the organization
2. **Action 2**: How to use these insights
3. **Action 3**: What additional data or resources would help

## Files in This Contribution

```
your_name_analysis/
├── README.md (this file)
├── notebooks/
│   ├── DataExploration.ipynb
├── scripts/
├── visualizations/
├── results/
│   ├── summary_statistics.csv
└── data/ (if applicable - only small derived datasets)
    ├── allstemcounter_output.csv
    ├── possiblefinanceinexistingquestions.csv
```

## How to Run This Analysis

### Prerequisites
```bash
conda install pandas, numpy, matplotlib, seaborn, nltk, collections, regex  
```

### Running the Analysis
```bash
# Navigate to the cnmetzi folder
cd datakit-smallholder-farmers-fall-2025/Challenge 5_ Financial Inclusion/cnmetzi/

# Start Jupyter Notebook
jupyter notebook

# Open and run notebooks in order:
# 1. 01_data_exploration.ipynb
# 2. 02_data_cleaning.ipynb
# 3. 03_analysis.ipynb
```

## References and Resources

### Academic Papers
N/A

### Datasets
Producers Direct dataset

### Tools and Libraries
anyio                     4.10.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
argon2-cffi               21.3.0             pyhd3eb1b0_0    https://repo.anaconda.com/pkgs/main
argon2-cffi-bindings      25.1.0          py311h02ab6af_0    https://repo.anaconda.com/pkgs/main
asttokens                 3.0.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
async-lru                 2.0.5           py311haa95532_0    https://repo.anaconda.com/pkgs/main
attrs                     25.4.0          py311haa95532_2    https://repo.anaconda.com/pkgs/main
babel                     2.17.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
beautifulsoup4            4.14.2          py311haa95532_0    https://repo.anaconda.com/pkgs/main
blas                      1.0                         mkl    https://repo.anaconda.com/pkgs/main
bleach                    6.3.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
bottleneck                1.4.2           py311h540bb41_1    https://repo.anaconda.com/pkgs/main
brotlicffi                1.1.0.0         py311h885b0b7_0    https://repo.anaconda.com/pkgs/main
bzip2                     1.0.8                h2bbff1b_6    https://repo.anaconda.com/pkgs/main
ca-certificates           2025.11.4            haa95532_0    https://repo.anaconda.com/pkgs/main
cairo                     1.18.4               he9e932c_0    https://repo.anaconda.com/pkgs/main
certifi                   2025.11.12      py311haa95532_0    https://repo.anaconda.com/pkgs/main
cffi                      2.0.0           py311h02ab6af_1    https://repo.anaconda.com/pkgs/main
charset-normalizer        3.4.4           py311haa95532_0    https://repo.anaconda.com/pkgs/main
colorama                  0.4.6           py311haa95532_0    https://repo.anaconda.com/pkgs/main
comm                      0.2.3           py311haa95532_0    https://repo.anaconda.com/pkgs/main
contourpy                 1.3.3           py311h214f63a_0    https://repo.anaconda.com/pkgs/main
cycler                    0.11.0             pyhd3eb1b0_0    https://repo.anaconda.com/pkgs/main
debugpy                   1.8.16          py311h885b0b7_1    https://repo.anaconda.com/pkgs/main
decorator                 5.2.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
defusedxml                0.7.1              pyhd3eb1b0_0    https://repo.anaconda.com/pkgs/main
executing                 2.2.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
expat                     2.7.3                h9214b88_0    https://repo.anaconda.com/pkgs/main
fontconfig                2.15.0               hd211d86_0    https://repo.anaconda.com/pkgs/main
fonttools                 4.60.1          py311h02ab6af_0    https://repo.anaconda.com/pkgs/main
freetype                  2.13.3               h0620614_0    https://repo.anaconda.com/pkgs/main
graphite2                 1.3.14               hd77b12b_1    https://repo.anaconda.com/pkgs/main
h11                       0.16.0          py311haa95532_1    https://repo.anaconda.com/pkgs/main
harfbuzz                  10.2.0               he2f9f60_1    https://repo.anaconda.com/pkgs/main
html5lib                  1.1                pyhd3eb1b0_0    https://repo.anaconda.com/pkgs/main
httpcore                  1.0.9           py311haa95532_0    https://repo.anaconda.com/pkgs/main
httpx                     0.28.1          py311haa95532_1    https://repo.anaconda.com/pkgs/main
icu                       73.1                 h6c2663c_0    https://repo.anaconda.com/pkgs/main
idna                      3.11            py311haa95532_0    https://repo.anaconda.com/pkgs/main
intel-openmp              2025.0.0          haa95532_1164    https://repo.anaconda.com/pkgs/main
ipykernel                 6.31.0          py311h4442805_0    https://repo.anaconda.com/pkgs/main
ipython                   9.7.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
ipython_pygments_lexers   1.1.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
ipywidgets                8.1.7           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jedi                      0.19.2          py311haa95532_0    https://repo.anaconda.com/pkgs/main
jinja2                    3.1.6           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jpeg                      9f                   ha349fce_0    https://repo.anaconda.com/pkgs/main
json5                     0.12.1          py311haa95532_0    https://repo.anaconda.com/pkgs/main
jsonschema                4.25.0          py311haa95532_1    https://repo.anaconda.com/pkgs/main
jsonschema-specifications 2025.9.1        py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter                   1.1.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter-lsp               2.2.5           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter_client            8.6.3           py311haa95532_1    https://repo.anaconda.com/pkgs/main
jupyter_console           6.6.3           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter_core              5.8.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter_events            0.12.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter_server            2.16.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyter_server_terminals  0.5.3           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyterlab                4.4.7           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyterlab_pygments       0.3.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyterlab_server         2.28.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
jupyterlab_widgets        3.0.15          py311haa95532_0    https://repo.anaconda.com/pkgs/main
kiwisolver                1.4.9           py311h03f52e7_0    https://repo.anaconda.com/pkgs/main
lcms2                     2.16                 hb4a4139_0    https://repo.anaconda.com/pkgs/main
lerc                      3.0                  hd77b12b_0    https://repo.anaconda.com/pkgs/main
libdeflate                1.17                 h2bbff1b_1    https://repo.anaconda.com/pkgs/main
libffi                    3.4.4                hd77b12b_1    https://repo.anaconda.com/pkgs/main
libglib                   2.84.4               hfaec014_0    https://repo.anaconda.com/pkgs/main
libiconv                  1.16                 h2bbff1b_3    https://repo.anaconda.com/pkgs/main
libkrb5                   1.21.3               h885b0b7_4    https://repo.anaconda.com/pkgs/main
libpng                    1.6.50               h46444df_0    https://repo.anaconda.com/pkgs/main
libpq                     17.6                 h652a1e2_0    https://repo.anaconda.com/pkgs/main
libsodium                 1.0.20               h83e8143_0    https://repo.anaconda.com/pkgs/main
libtiff                   4.5.1                hd77b12b_0    https://repo.anaconda.com/pkgs/main
libwebp-base              1.6.0                hbf3958f_0    https://repo.anaconda.com/pkgs/main
libxml2                   2.13.9               h6201b9f_0    https://repo.anaconda.com/pkgs/main
libzlib                   1.3.1                h02ab6af_0    https://repo.anaconda.com/pkgs/main
lz4-c                     1.9.4                h2bbff1b_1    https://repo.anaconda.com/pkgs/main
markupsafe                3.0.2           py311h827c3e9_0    https://repo.anaconda.com/pkgs/main
matplotlib                3.10.6          py311haa95532_1    https://repo.anaconda.com/pkgs/main
matplotlib-base           3.10.6          py311h43afe63_1    https://repo.anaconda.com/pkgs/main
matplotlib-inline         0.2.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
mistune                   3.1.2           py311haa95532_0    https://repo.anaconda.com/pkgs/main
mkl                       2025.0.0           h5da7b33_930    https://repo.anaconda.com/pkgs/main
mkl-service               2.5.2           py311h0b37514_0    https://repo.anaconda.com/pkgs/main
mkl_fft                   2.1.1           py311h300f80d_0    https://repo.anaconda.com/pkgs/main
mkl_random                1.3.0           py311ha5e6156_0    https://repo.anaconda.com/pkgs/main
mysql-common              9.3.0                hf582a5b_3    https://repo.anaconda.com/pkgs/main
mysql-libs                9.3.0                hc0ebf12_3    https://repo.anaconda.com/pkgs/main
narwhals                  2.7.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
nbclient                  0.10.2          py311haa95532_0    https://repo.anaconda.com/pkgs/main
nbconvert                 7.16.6          py311haa95532_0    https://repo.anaconda.com/pkgs/main
nbconvert-core            7.16.6          py311haa95532_0    https://repo.anaconda.com/pkgs/main
nbconvert-pandoc          7.16.6          py311haa95532_0    https://repo.anaconda.com/pkgs/main
nbformat                  5.10.4          py311haa95532_0    https://repo.anaconda.com/pkgs/main
nest-asyncio              1.6.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
notebook                  7.4.5           py311haa95532_0    https://repo.anaconda.com/pkgs/main
notebook-shim             0.2.4           py311haa95532_0    https://repo.anaconda.com/pkgs/main
numexpr                   2.14.1          py311h7660c64_0    https://repo.anaconda.com/pkgs/main
numpy                     2.3.5           py311h050da96_0    https://repo.anaconda.com/pkgs/main
numpy-base                2.3.5           py311h1e017a8_0    https://repo.anaconda.com/pkgs/main
openjpeg                  2.5.2                hae555c5_0    https://repo.anaconda.com/pkgs/main
openssl                   3.0.18               h543e019_0    https://repo.anaconda.com/pkgs/main
overrides                 7.7.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
packaging                 25.0            py311haa95532_1    https://repo.anaconda.com/pkgs/main
pandas                    2.3.3           py311h42c1672_1    https://repo.anaconda.com/pkgs/main
pandoc                    3.8                  haa95532_0    https://repo.anaconda.com/pkgs/main
pandocfilters             1.5.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
parso                     0.8.5           py311haa95532_0    https://repo.anaconda.com/pkgs/main
pcre2                     10.46                h5740b90_0    https://repo.anaconda.com/pkgs/main
pillow                    11.1.0          py311h096bfcc_0    https://repo.anaconda.com/pkgs/main
pip                       25.3               pyhc872135_0    https://repo.anaconda.com/pkgs/main
pixman                    0.46.4               h4043f72_0    https://repo.anaconda.com/pkgs/main
platformdirs              4.5.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
plotly                    6.3.0           py311hbc747e5_0    https://repo.anaconda.com/pkgs/main
prometheus_client         0.21.1          py311haa95532_0    https://repo.anaconda.com/pkgs/main
prompt-toolkit            3.0.52          py311haa95532_1    https://repo.anaconda.com/pkgs/main
prompt_toolkit            3.0.52               hd3eb1b0_1    https://repo.anaconda.com/pkgs/main
psutil                    7.0.0           py311h02ab6af_1    https://repo.anaconda.com/pkgs/main
pure_eval                 0.2.3           py311haa95532_0    https://repo.anaconda.com/pkgs/main
pycparser                 2.23            py311haa95532_0    https://repo.anaconda.com/pkgs/main
pygments                  2.19.2          py311haa95532_0    https://repo.anaconda.com/pkgs/main
pyparsing                 3.2.5           py311haa95532_0    https://repo.anaconda.com/pkgs/main
pyqt                      6.9.1           py311h12ec796_0    https://repo.anaconda.com/pkgs/main
pyqt6-sip                 13.10.2         py311h630b2a1_0    https://repo.anaconda.com/pkgs/main
pysocks                   1.7.1           py311haa95532_1    https://repo.anaconda.com/pkgs/main
python                    3.11.14              h981015d_0    https://repo.anaconda.com/pkgs/main
python-dateutil           2.9.0post0      py311haa95532_2    https://repo.anaconda.com/pkgs/main
python-fastjsonschema     2.21.2          py311haa95532_0    https://repo.anaconda.com/pkgs/main
python-json-logger        3.2.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
python-tzdata             2025.2             pyhd3eb1b0_0    https://repo.anaconda.com/pkgs/main
pytz                      2025.2          py311haa95532_0    https://repo.anaconda.com/pkgs/main
pywin32                   311             py311h885b0b7_0    https://repo.anaconda.com/pkgs/main
pywinpty                  2.0.15          py311h72d21ff_0    https://repo.anaconda.com/pkgs/main
pyyaml                    6.0.3           py311hb9a58be_0    https://repo.anaconda.com/pkgs/main
pyzmq                     27.1.0          py311h7149c55_1    https://repo.anaconda.com/pkgs/main
qtbase                    6.9.2                hd965823_2    https://repo.anaconda.com/pkgs/main
qtconsole                 5.7.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
qtdeclarative             6.9.2                h88b4c33_1    https://repo.anaconda.com/pkgs/main
qtpy                      2.4.3           py311haa95532_0    https://repo.anaconda.com/pkgs/main
qtsvg                     6.9.2                h30ace32_1    https://repo.anaconda.com/pkgs/main
qttools                   6.9.2                h7e7b719_1    https://repo.anaconda.com/pkgs/main
qtwebchannel              6.9.2                heb02b0b_1    https://repo.anaconda.com/pkgs/main
qtwebsockets              6.9.2                heb02b0b_1    https://repo.anaconda.com/pkgs/main
referencing               0.37.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
requests                  2.32.5          py311haa95532_1    https://repo.anaconda.com/pkgs/main
rfc3339-validator         0.1.4           py311haa95532_0    https://repo.anaconda.com/pkgs/main
rfc3986-validator         0.1.1           py311haa95532_0    https://repo.anaconda.com/pkgs/main
rpds-py                   0.28.0          py311h114bc41_0    https://repo.anaconda.com/pkgs/main
seaborn                   0.13.2          py311haa95532_3    https://repo.anaconda.com/pkgs/main
send2trash                1.8.2           py311haa95532_1    https://repo.anaconda.com/pkgs/main
setuptools                80.9.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
sip                       6.12.0          py311h706e071_0    https://repo.anaconda.com/pkgs/main
six                       1.17.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
sniffio                   1.3.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
soupsieve                 2.5             py311haa95532_0    https://repo.anaconda.com/pkgs/main
sqlite                    3.51.0               hda9a48d_0    https://repo.anaconda.com/pkgs/main
stack_data                0.6.3           py311haa95532_0    https://repo.anaconda.com/pkgs/main
tbb                       2022.0.0             h214f63a_0    https://repo.anaconda.com/pkgs/main
tbb-devel                 2022.0.0             h214f63a_0    https://repo.anaconda.com/pkgs/main
terminado                 0.18.1          py311haa95532_0    https://repo.anaconda.com/pkgs/main
tinycss2                  1.4.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
tk                        8.6.15               hf199647_0    https://repo.anaconda.com/pkgs/main
tornado                   6.5.1           py311h827c3e9_0    https://repo.anaconda.com/pkgs/main
traitlets                 5.14.3          py311haa95532_0    https://repo.anaconda.com/pkgs/main
typing-extensions         4.15.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
typing_extensions         4.15.0          py311haa95532_0    https://repo.anaconda.com/pkgs/main
tzdata                    2025b                h04d1e81_0    https://repo.anaconda.com/pkgs/main
ucrt                      10.0.22621.0         haa95532_0    https://repo.anaconda.com/pkgs/main
urllib3                   2.5.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
vc                        14.3                h2df5915_10    https://repo.anaconda.com/pkgs/main
vc14_runtime              14.44.35208         h4927774_10    https://repo.anaconda.com/pkgs/main
vs2015_runtime            14.44.35208         ha6b5a95_10    https://repo.anaconda.com/pkgs/main
wcwidth                   0.2.13          py311haa95532_0    https://repo.anaconda.com/pkgs/main
webencodings              0.5.1           py311haa95532_1    https://repo.anaconda.com/pkgs/main
websocket-client          1.8.0           py311haa95532_0    https://repo.anaconda.com/pkgs/main
wheel                     0.45.1          py311haa95532_0    https://repo.anaconda.com/pkgs/main
widgetsnbextension        4.0.14          py311haa95532_0    https://repo.anaconda.com/pkgs/main
win_inet_pton             1.1.0           py311haa95532_1    https://repo.anaconda.com/pkgs/main
winpty                    0.4.3                         4    https://repo.anaconda.com/pkgs/main
xz                        5.6.4                h4754444_1    https://repo.anaconda.com/pkgs/main
yaml                      0.2.5                he774522_0    https://repo.anaconda.com/pkgs/main
zeromq                    4.3.5                h6c54ac7_1    https://repo.anaconda.com/pkgs/main
zlib                      1.3.1                h02ab6af_0    https://repo.anaconda.com/pkgs/main
zstd                      1.5.7   

## Contact and Collaboration

**Author**: Camille
**GitHub**: @cnmetzi
**Slack**: @Camille

**Collaboration Welcome**: 
- Open to feedback and suggestions
- Happy to collaborate on related analyses
- Available to answer questions about this approach

## Acknowledgments

Thank you to DataKind for facilitating this DataKit
This example submission template and clear instructions in the brief made things much easier when volunteering for a limited time asyncronously

---

**Last Updated**: 12/5/25
**Status**: Needs Review

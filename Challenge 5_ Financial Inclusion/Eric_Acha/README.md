# Juan Eric Acha - Challenge 5: Financial Inclusion Analysis

## Overview
This analysis explores text-based communication data from smallholder farmers owned by Producers Direct. The primary objective is to understand their economic realities, common financial terminology, and to find financial inclusion opportunities for them. The insights derived are crucial for identifying specific opportunities to improve financial inclusion within this community, allowing Producers Direct to tailor support mechanisms, educational resources, and potential financial product partnerships to better meet farmer needs.

## Research Questions
- Question 1: What are the economic realities of farmers? 
- Question 2: What are the key financial terms farmers use in their conversations, and what are the most common terms that coincide?
- Question 3: What areas are farmer most interested in spending more financial resources in? What opportunities are there for financial inclusion?

## Methodology

### Data Sources
- Small Farmers' Text Data From Producers Ditect
- Document any data preprocessing steps

### Approach
1. **Step 1**: Data loading and initial exploration
2. **Step 2**: Data cleaning and preprocessing
3. **Step 3**: Analysis techniques applied
4. **Step 4**: Visualization and interpretation
5. **Step 5**: Validation and testing

### Tools and Technologies
- **Programming Language**: Python 3.x
- **Key Libraries**: pandas, numpy, matplotlib, seaborn, scikit-learn, spacy.
- **GenAI Tools Used**: Gemini
- **Other Tools**: Jupyter Notebook, Tableau.

## Use of Generative AI

### Tools Used
- **Gemini**: Generating initial code structure for data loading, cleaning, and processing.

### Human Review Process
- All AI-generated code was reviewed and tested for accuracy
- AI-generated insights were validated against the data

### AI-Assisted vs. Human-Created
- **AI-Assisted**: Initial data translation and visualization code structure
- **Human-Created**: All analysis logic, interpretation, and conclusions

## Key Findings

### Finding 1: [Dispite Differences In Languages and Region, Most Small Farmers Have Similar Needs]
Farmers were initially paired into groups. Those who spoke mainly English via text and those who spoke Swahili, Luganda, or Nyn. Both groups ask questions about the same topics regardless of the language differences. This trend was seen in the word cloud in visual 1A where the biggest words point to crops and caddle. This is further supported by the vizual 1B where word counts reveal the precise crop and caddle most farmers usually in inquire about

**Implications for Producers Direct:**
This finding suggest Producers Direct should focus on translating potential farming guides to multiple different languages as sopposed to rewriting guides to appeal to a particular language or territory. 

### Finding 2: [Most Small Farmers Can Benefit From Different Financial Products]
Farmers can use financial resources to improve their crops and caddle. Many farmers in their conversations associate money and loans with their crops and caddle as shown in visual 2. Maize and cow are the two words with the highest co-ocurrence for loans and money. These words represent crops and caddle, suggesting farmers' needs for loan and money around these resources

**Implications for Producers Direct:**
This finding suggest there is room for Producers Direct to improve farmers' financial inclusion. First by educating farmers through Farmers Guides, courses, wordshops, etc... so they learn further about what to grow and how to grow it. And second, partnering with local banks and finding loans for the farmers who produce the highest profit.

## Visualizations

### [Word Cloud]
![Visualization 1A](Visuals/visual1a.png)

**Interpretation**: This graphs show the most common words in the text visually. It shows the constrast between translated and non-translated text

### [Word Frequency Graph]
![Visualization 1B](Visuals/visual1b.png)

**Interpretation**: This graph shows the frequency count for the most common words. It assist in providing more granular detail about words' commonalities 

### [Network Keyword Graph]
![Visualization 2](Visuals/visual2.png)

**Interpretation**: This graph shows the main financial inclusion keywords found in the text along side their most co-occuring words. This aids in identifying the type of financial inclusion keywords used in the text and the context in which they are used

## Limitations and Challenges

### Methodological Limitations
- Simplifications required
   - English questions are geared towards the same topics as other languages
   - Over 2000 characters were translated to English but only questions written in English were used for most of the analysis
- Alternative approaches not explored
    -  A sample of a few thousand characters translated may not provide greater insight than just collecting the questions that are already in English. However, exploring a sample with at least 10 million characters translated from other languages may uncover additional insight

### Technical Challenges
- Computational constraints
    - Only sample of 2000 translated character could be generated
- Translation accuracy issues
    - There is a lot of nuance that can be missed by Google Translate. Implementing and testing other model may provide greater insights


## Contact and Collaboration

**Author**: [Juan Eric Acha]
**GitHub**: @juaneacha

**Collaboration Welcome**: 
- Open to feedback and suggestions
- Happy to collaborate on related analyses
- Available to answer questions about this approach

**Last Updated**: [12/7/2025]
**Status**: [Complete]

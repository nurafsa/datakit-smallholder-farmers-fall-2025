# Data Cleaning – Data Preparation Stage

This document describes the process of preparing data used in subsequent stages of word analysis and dictionary construction for the following languages:
- Luganda (`lug`),
- Runyankole (`nyn`),
- Kiswahili (`swa`),
- English (`eng`).

The steps were performed primarily in Power Query, and the resulting data is used in Jupyter notebooks (`*_word_frequency.ipynb`).

---

# 1. Downloading the Source Data

The input data was downloaded from a public URL provided in the Producers Direct project documentation.

The downloaded file was saved locally as:

**`raw_challenge_2_seasonality.csv`**

The file contains the complete set of agricultural question records, including user metadata, response information, question language (`question_language`), and topic field (`question_topic`).

---

# 2. Loading the Data into Power Query

The file `raw_challenge_2_seasonality.csv` was imported into Power Query to perform initial cleaning and data preparation.

At this stage:
- column names and data types were identified,
- key fields (including `question_language`, `question_topic`, and the question text) were verified to be available,
- the dataset was prepared for further column reduction and deduplication.

---

# 3. Removing Unnecessary Columns

In the first cleaning step, columns that were not needed for further text analysis or contained detailed user and response metadata were removed.

The Power Query operation used:

```m
= Table.RemoveColumns(#"Changed Type",
{
    "question_user_gender", "response_user_gender", "response_id",
    "response_user_id", "response_language", "response_content",
    "response_topic", "response_user_type", "response_user_status",
    "response_user_country_code", "response_user_dob",
    "response_user_created_at", "question_user_dob",
    "question_user_type", "question_user_status",
    "question_user_created_at", "response_sent",
    "question_user_id"
})
```

The purpose of this step:
- reducing the size of the table,
- removing fields that are not used in further linguistic analysis,
- limiting the data scope to information that is actually needed in the next stage (analysis of question content, language, topic).

---

# 4. Removing Duplicates

After removing unnecessary columns, deduplication was performed at the level of the entire table:
```m
= Table.Distinct(#"Removed Columns")
```

As a result:
- duplicate question records were eliminated,
- it was ensured that word frequency analysis and subsequent statistics would not be distorted by counting the same observations multiple times.

---

# 5. Creating the `topic_category` Column (Working Thematic Categorization)

To facilitate a possible thematic breakdown in later visualizations (e.g., on a dashboard) and data exploration, a new **`topic_category`** column was created.

**Important assumption:**  
The set of categories does **not** come from the source data or the official Producers Direct taxonomy.  
The categories were **defined independently for the purposes of this analysis** as a working, simplified thematic breakdown of agricultural questions.

The logic for creating the `topic_category` column included normalizing `question_topic` and matching it against prepared working lists of categories such as: cereals, legumes, vegetables, fruits, roots_tubers, livestock, cash_crops, fodder_forage, trees.  
Questions that did not fit into any category were assigned the label `"other/unknown"`.

Below is the code (M language / Power Query) used to create this column:

```m
let
    topic =
        if [question_topic] = null then
            null
        else
            Text.Lower(Text.Trim([question_topic])),

    cereals = {
        "maize", "wheat", "barley", "rice",
        "millet", "finger-millet", "oat", "rye", "cereal"
    },

    legumes = {
        "bean", "pea", "cowpea", "pigeon-pea", "pigeon",
        "chickpea", "mung-bean", "soya", "lupin",
        "snap-pea", "snow-pea", "french-bean", "peanut"
    },

    vegetables = {
        "amaranth", "asparagus", "aubergine", "beetroot",
        "broccoli", "butternut-squash", "cabbage", "carrot",
        "cauliflower", "celery", "chard", "chilli",
        "collard-greens", "courgette", "cucumber",
        "garlic", "ginger", "greens", "kale", "leek",
        "lettuce", "okra", "onion", "parsley",
        "pumpkin", "radish", "spinach", "squash",
        "tomato", "vegetable",
        "nightshade", "black-nightshade", "african-nightshade",
        "capsicum", "corriander"
    },

    fruits = {
        "apple", "apricot", "avocado", "banana", "blackberry",
        "cranberry", "gooseberry", "grape", "guava",
        "jackfruit", "lemon", "mango", "melon", "mulberry",
        "olive", "orange", "passion-fruit", "paw-paw",
        "peach", "pear", "pineapple", "strawberry",
        "watermelon"
    },

    roots_tubers = {
        "cassava", "sweet-potato", "potato", "taro", "yam"
    },

    livestock = {
        "animal", "cattle", "goat", "sheep", "pig",
        "poultry", "chicken", "duck", "turkey",
        "rabbit", "fish", "tilapia", "ostrich",
        "guinea-fowl", "guinea-pig", "bee", "camel",
        "livestock"
    },

    cash_crops = {
        "coffee", "tea", "cocoa", "cotton", "tobacco",
        "cashew-nut", "macademia", "castor-bean",
        "flax", "pyrethrum", "miraa", "sisal",
        "rapeseed", "sesame", "sunflower", "safflower",
        "sugar-cane", "chia"
    },

    fodder_forage = {
        "boma-rhodes", "brachiaria-grass", "grass",
        "napier-grass", "sudan-grass", "setaria",
        "lucern", "desmodium", "clover",
        "leucaena", "caliandra", "purple-vetch", "vetch"
    },

    trees = {
        "acacia", "bamboo", "eucalyptus", "tree", "cyprus"
    }

in
    if topic = null or topic = "" then
        "other/unknown"
    else if List.Contains(cereals, topic) then
        "cereals"
    else if List.Contains(legumes, topic) then
        "legumes"
    else if List.Contains(vegetables, topic) then
        "vegetables"
    else if List.Contains(fruits, topic) then
        "fruits"
    else if List.Contains(roots_tubers, topic) then
        "roots_tubers"
    else if List.Contains(livestock, topic) then
        "livestock"
    else if List.Contains(cash_crops, topic) then
        "cash_crops"
    else if List.Contains(fodder_forage, topic) then
        "fodder_forage"
    else if List.Contains(trees, topic) then
        "trees"
    else
        "other/unknown"
```

---

# 6. Creating Language Tables (Reference in Power Query)

After completing the cleaning steps (removing columns, deduplication, adding `topic_category`), the data was split into separate tables for each language using the **Reference** function, so that all tables inherit the same cleaning logic.

The following were created:
- `raw_seasonality_lug` – `question_language = "lug"`
- `raw_seasonality_nyn` – `question_language = "nyn"`
- `raw_seasonality_swa` – `question_language = "swa"`
- `raw_seasonality_eng` – `question_language = "eng"`

---

# 7. Purpose of Splitting the Data by Language

Splitting the data into four separate tables is crucial for the subsequent analysis:
- it enables running separate cleaning and word analysis pipelines,
- it simplifies managing language-specific stop-word lists,
- it makes it easier to compare vocabulary structures across languages.

Each table inherits:
- identical cleaning steps,
- the same logic for creating `topic_category`,
- a structure consistent with the given language.

---

# 8. Word Analysis in Jupyter Notebooks and Cleaning with GPT

The language tables prepared in Power Query (`raw_seasonality_eng`, `raw_seasonality_lug`, `raw_seasonality_nyn`, `raw_seasonality_swa`) are exported to CSV files and used as input in the notebooks:

- `ang_word_frequency.ipynb`  
- `lug_word_frequency.ipynb`  
- `nyn_word_frequency.ipynb`  
- `swa_word_frequency.ipynb`  

The goal of this stage is:
- to build ordered lists of words occurring in the questions,  
- to filter out low-information words (stop words, general vocabulary, words unrelated to the thematic categories),  
- to prepare lists of candidate words for the classification dictionary, using the GPT model (ChatGPT) for semi-automatic selection.

The process is identical for all four languages; only the input/output file names differ.

---

## 8.1. Stage 1 – Generating the Initial Frequency List (Top 3000 Words)

### Input (example: ENG):
- file: `questions_eng.csv`  

### Steps in the notebook:

1. **Loading the data**  
   Loading the CSV file into a pandas DataFrame.

2. **Text cleaning**  
   - lowercase  
   - removal of non-letter characters (regEx)  
   - whitespace reduction  
   - ignoring empty values  

3. **Tokenization**  
   Each question is split into unique tokens (words) to avoid counting the same word multiple times within a single question.

4. **Counting frequency**  
   For each word, the number of questions in which it appears is calculated.

5. **Ranking and saving Top 3000**  
   The result is saved to:
   - `eng_top_words.csv`
   - analogously: `lug_top_words.csv`, `nyn_top_words.csv`, `swa_top_words.csv`

## 8.2. Semi-automatic List Cleaning Using the GPT Model

The `*_top_words.csv` files are analyzed with the help of ChatGPT in order to:
- identify words *not related* to the thematic categories,
- filter out low-information words,
- create a list of custom stop words.

### Procedure

1. **Exporting the Top 3000 list to GPT**  
   For each language, the list of approximately 3000 most frequent words (`*_top_words.csv`) is exported and passed to ChatGPT.

2. **Providing the thematic categories**  
   Along with the word list, GPT receives a description of the working categories to which the questions will ultimately be assigned.  
   The categories follow the same logic later used in the Power Query code and include, among others:

   - **`market_price`** – questions about prices, selling, buying, units, market (prices / markets / selling),  
   - **`planting_growing`** – planting, sowing, cultivation, seeds, soil, crop growth, fertilizers,  
   - **`livestock`** – animal husbandry (cows, chickens, goats, pigs, etc.), feeding, keeping,  
   - **`pests_disease`** – pests, plant and animal diseases, control measures, spraying, treatment,  
   - **`timing_harvest`** – timing, ripening, harvest, yield, breeding periods, etc.,  
   - **`weather`** – weather, rain, drought, sun, seasons and seasonality,  
   - default category **`other/unknown`** – for words that cannot be reliably assigned to any of the above.

   GPT’s task is to **indicate the words that it is NOT able to clearly assign to any of these categories** – these words are added to the “non-category” list.

3. **Saving the “non-category” word list**  
   Words classified by GPT as:
   - too general,
   - uninformative,
   - unrelated to the thematic categories above

   are saved in the files:

   - `eng_non_category_words.csv`
   - `lug_non_category_words.csv`
   - `nyn_non_category_words.csv`
   - `swa_non_category_words.csv`

The `*_non_category_words.csv` list serves as an extended, contextual stop-word list for a given language. In the next stage (8.3), it is used to filter out these words before determining the next ~5000 most informative terms.

---

## 8.3. Stage 2 – Applying the Stop-word List and Determining the Next ~5000 Words

### Input:
- full table for the language (`questions_eng.csv`),
- and the stop-word list (`eng_non_category_words.csv`).

### Steps:

1. **Reloading the data**  
2. **Repeating text cleaning** – the same function as before  
3. **Loading the stop-word list**  
4. **Filtering tokens** – removing words from the list  
5. **Recalculating frequencies**  
6. **Saving the next ~5000 words after filtering** as:
   - `eng_next5000_words.csv`
   - `lug_next5000_words.csv`
   - `nyn_next5000_words.csv`
   - `swa_next5000_words.csv`

This list contains words with higher informational value.

---

## 8.4. Role of the Generated Lists in Subsequent Stages and Question Classification with GPT

As a result, for each language a set of three key intermediate files is created:

- `*_top_words.csv` — most frequent words before filtering (Top ~3000),  
- `*_non_category_words.csv` — words indicated by GPT as low-information or unrelated to the agricultural domain,  
- `*_next5000_words.csv` — the next words (~5000) after stop-word filtering.

These sets serve as input to the next stage, whose goal is **classification of words and entire questions into working thematic categories**, carried out using the GPT model.  
Thanks to this, it is possible to build dictionaries for further analyses and to automatically assign thematic categories in Power Query.

### Word classification using GPT

1. The full list of words `*_next5000_words.csv` was passed to GPT together with a description of the working categories corresponding to typical types of agricultural questions, including:

   - **`market_price`** — prices, selling, buying, units, market,  
   - **`planting_growing`** — planting, sowing, cultivation, seeds, soil, fertilizers,  
   - **`livestock`** — animal husbandry, feeding, keeping,  
   - **`pests_disease`** — pests, diseases, control measures, spraying, treatment,  
   - **`timing_harvest`** — timing, ripening, harvest, yield, breeding periods,  
   - **`weather`** — weather, rain, drought, sun, seasonality,  
   - default category **`other` / `other/unknown`** — for words without an unambiguous match.

2. Based on the `*_next5000_words.csv` file and the description of thematic categories, GPT generated a ready-made M code snippet with keyword lists for each category (including `LUG_Q_MARKET_PRICE`, `LUG_Q_PLANTING_GROWING`, `LUG_Q_LIVESTOCK`, `LUG_Q_PESTS_DISEASE`, `LUG_Q_TIMING_HARVEST`, `LUG_Q_WEATHER`). Below is an example of such code for the English language, which was then used directly to build the question classification column in Power Query.

```m
// =============== 1) Prices / markets / selling ===============
    ENG_Q_MARKET_PRICE = {
        "price", "prices",
        "market", "markets",
        "sell", "selling",
        "buy", "buying",
        "cost", "costs",
        "profit", "profits",
        "income",
        "kilo", "kilogram", "kilograms",
        "bag", "bags", "sack", "sacks"
    },

    // =============== 2) Planting / growing crops ===============
    ENG_Q_PLANTING_GROWING = {
        // farming / cultivation
        "plant", "plants", "planting",
        "sow", "sowing",
        "germinate", "germination",
        "grow", "growing", "growth",
        "farm", "farms", "farming",
        "farmer", "farmers",
        "land", "soil",
        "field", "fields",
        "acre", "acres",
        "weed", "weeds", "weeding",
        "spacing",
        "mulching",
        "pruning",
        // fertilizer / inputs
        "fertilizer", "fertiliser",
        "manure", "compost", "dung",
        "urea", "dap", "can", "npk",
        "input", "inputs",
        // crop names as context of growing
        "maize", "corn",
        "beans", "bean",
        "banana", "bananas",
        "plantain",
        "cassava",
        "coffee", "tea",
        "sorghum", "millet",
        "rice", "paddy",
        "potato", "potatoes",
        "tomato", "tomatoes",
        "cabbage", "cabbages",
        "onion", "onions",
        "groundnut", "groundnuts",
        "sunflower", "sunflowers",
        "simsim", "sesame",
        "sugarcane",
        "yam", "yams",
        "vegetable", "vegetables",
        "soybean", "soybeans",
        "fruit", "fruits",
        "avocado", "avocados",
        "orange", "oranges",
        "mango", "mangoes",
        "pawpaw", "papaya"
    },

    // =============== 3) Livestock ===============
    ENG_Q_LIVESTOCK = {
        "cow", "cows",
        "goat", "goats",
        "sheep",
        "pig", "pigs",
        "cattle",
        "chicken", "chickens",
        "hen", "hens",
        "broiler", "broilers",
        "layers",
        "chick", "chicks",
        "turkey", "turkeys",
        "duck", "ducks",
        "rabbit", "rabbits",
        "fish", "tilapia", "catfish",
        "poultry",
        "heifer", "heifers",
        "bull", "bulls",
        "calf", "calves"
    },

    // =============== 4) Pests / diseases / treatments ===============
    ENG_Q_PESTS_DISEASE = {
        // pests
        "pest", "pests",
        "aphid", "aphids",
        "borer", "borers",
        "weevil", "weevils",
        "mite", "mites",
        "tick", "ticks",
        "worm", "worms",
        "lice", "louse",
        // diseases / problems
        "disease", "diseases",
        "fungus", "fungi",
        "rot", "rots", "rotten",
        "wilt", "wiltering",
        "blight",
        "virus",
        "bacteria",
        "nematode",
        "coccidiosis",
        "newcastle",
        "mastitis",
        "diarrhoea", "diarrhea",
        // treatments / chemicals
        "spray", "spraying",
        "herbicide",
        "pesticide",
        "insecticide",
        "drug", "drugs",
        "vaccine", "vaccination",
        "treat", "treatment",
        "control"
    },

    // =============== 5) Time / maturity / harvest ===============
    ENG_Q_TIMING_HARVEST = {
        // time / duration
        "day", "days",
        "week", "weeks",
        "month", "months",
        "year", "years",
        "season", "seasons",
        "time", "period",
        // maturity / harvest
        "harvest", "harvesting",
        "yield", "yields",
        "mature", "maturity",
        "ripe", "ripen"
    },

    // =============== 6) Weather / season / climate ===============
    ENG_Q_WEATHER = {
        "rain", "rains", "rainfall",
        "drought",
        "sun", "sunshine",
        "hot", "heat",
        "cold",
        "frost",
        "dry", "wet",
        "climate",
        "flood", "floods", "flooding"
    },

```

3. The keyword lists returned by GPT were then used to build a column that classifies the **entire question** (`question_content`) in Power Query. For each language, a set of lists was prepared — such as `ENG_Q_MARKET_PRICE`, `ENG_Q_PLANTING_GROWING`, `ENG_Q_LIVESTOCK`, `ENG_Q_PESTS_DISEASE`, `ENG_Q_TIMING_HARVEST`, `ENG_Q_WEATHER` (analogously for the other languages). A helper function `ContainsAny` was then used to check whether the question text contains any word from a given list. Based on this, the question category is created (`"pests_disease"`, `"market_price"`, `"planting_growing"`, `"livestock"`, `"timing_harvest"`, `"weather"`, `"other"`).

Below is an example implementation of this logic for the **English** language:

```m
let
    t = 
        if [question_content] = null 
        then null 
        else Text.Lower(Text.Trim([question_content])),

    // Helper: check if text contains any keyword from a list
    ContainsAny = (txt as nullable text, keywords as list) as logical =>
        if txt = null then false 
        else 
            List.AnyTrue(
                List.Transform(
                    keywords, 
                    (k) => Text.Contains(txt, k, Comparer.OrdinalIgnoreCase)
                )
            ),

     // ================= KEYWORD LISTS (generated with GPT) =================
    // The full keyword lists used for classification are defined in the query:
    //   - ENG_Q_MARKET_PRICE
    //   - ENG_Q_PLANTING_GROWING
    //   - ENG_Q_LIVESTOCK
    //   - ENG_Q_PESTS_DISEASE
    //   - ENG_Q_TIMING_HARVEST
    //   - ENG_Q_WEATHER

    // =============== FINAL CATEGORY ASSIGNMENT ===============
    result =
        if t = null or t = "" then "other" else
        // priority: 1) pests/disease, 2) market, 3) planting/growing, 4) livestock, 5) timing/harvest, 6) weather
        if ContainsAny(t, ENG_Q_PESTS_DISEASE)      then "pests_disease"    else
        if ContainsAny(t, ENG_Q_MARKET_PRICE)       then "market_price"     else
        if ContainsAny(t, ENG_Q_PLANTING_GROWING)   then "planting_growing" else
        if ContainsAny(t, ENG_Q_LIVESTOCK)          then "livestock"        else
        if ContainsAny(t, ENG_Q_TIMING_HARVEST)     then "timing_harvest"   else
        if ContainsAny(t, ENG_Q_WEATHER)            then "weather"          else
        "other"
in
    result
```

## 9. Merging the Language Tables into the Final Structure (`proc_challenge_2_seasonality`)

After completing data cleaning, thematic classification, and creating the `topic_category` column in each language-specific table  
(`raw_seasonality_lug`, `raw_seasonality_nyn`, `raw_seasonality_swa`, `raw_seasonality_eng`), the data was merged back into a single unified dataset.

The merging was performed in Power Query using the **Append Queries** operation, combining all four tables into one structure:

### **`proc_challenge_2_seasonality`**

The tables were combined vertically (row-wise), as they shared an identical column layout:

- `question_id`  
- `question_language`  
- `question_content`  
- `question_topic`  
- `question_sent`  
- `question_user_country_code`  
- `topic_category` – category assigned based on the GPT-generated keyword dictionary  
- `topic_type` – information about the origin or type of classification (e.g., GPT / manual)

The final **`proc_challenge_2_seasonality`** table constitutes a complete and standardized dataset used in subsequent stages of analysis, modeling, and dashboard preparation.

---

The final CSV file **`proc_challenge_2_seasonality.csv`** will then be used to prepare an auxiliary pivot table, which serves exclusively as a data source for the Tableau dashboard.  
A detailed explanation of how the pivot table is constructed, along with a clear step-by-step description, will be provided in a separate file: **`seasonality_pivot_explained.md`**.
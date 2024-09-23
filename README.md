# ICIS Mathematical Formula for Entity Recognition Effectiveness

To assess the effectiveness of your entity recognition and determine how aligned our ICIS content is with user queries, with a little help, lots of testing and tweaking, and some help from ChatGPT, I created a mathematical formula that compares the entities extracted from both the content we publish and the questions users ask. Below are the steps to evaluate these metrics via a formula.

## 1. Extract Entities from Content and Queries

### a. Content Entities (C)

- Use the ICIS AI Annotator entity recognition tool to extract all entities (e.g., commodities, locations, companies) from the published content.
- For each entity, record:
  - **Type**: The category of the entity (e.g., Commodity, Location, Company).
  - **Text**: The actual name or term of the entity.
  - **Frequency**: The number of times the entity appears in the content.

### b. Query Entities (Q)

- Similarly, entities are extracted from user queries.
- Records the same information as above.

## 2. Calculate Frequencies and Normalize

For each entity <img src="https://i.upmath.me/svg/%5C(%20e%20%5C)" alt="\( e \)" />:

### a. Calculate Frequencies

- **Frequency in Content <img src="https://i.upmath.me/svg/(%5C(%20f_c(e)%20%5C))" alt="(\( f_c(e) \))" />**: The number of times entity <img src="https://i.upmath.me/svg/%5C(%20e%20%5C)" alt="\( e \)" /> appears in the content.
- **Frequency in Queries <img src="https://i.upmath.me/svg/(%5C(%20f_q(e)%20%5C))" alt="(\( f_q(e) \))" />**: The number of times entity <img src="https://i.upmath.me/svg/%5C(%20e%20%5C)" alt="\( e \)" /> appears in the queries.

### b. Normalize Frequencies

Calculate the total frequencies:

- **Total Content Frequency <img src="https://i.upmath.me/svg/(%5C(%20F_c%20%5C))" alt="(\( F_c \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20F_c%20%3D%20%5Csum_%7Be%7D%20f_c(e)%0A%20%20%5C%5D" alt="\[
  F_c = \sum_{e} f_c(e)
  \]" />

- **Total Query Frequency <img src="https://i.upmath.me/svg/(%5C(%20F_q%20%5C))" alt="(\( F_q \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20F_q%20%3D%20%5Csum_%7Be%7D%20f_q(e)%0A%20%20%5C%5D" alt="\[
  F_q = \sum_{e} f_q(e)
  \]" />

Normalize the individual frequencies:

- **Normalized Content Frequency <img src="https://i.upmath.me/svg/(%5C(%20P_c(e)%20%5C))" alt="(\( P_c(e) \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20P_c(e)%20%3D%20%5Cfrac%7Bf_c(e)%7D%7BF_c%7D%0A%20%20%5C%5D" alt="\[
  P_c(e) = \frac{f_c(e)}{F_c}
  \]" />

- **Normalized Query Frequency <img src="https://i.upmath.me/svg/(%5C(%20P_q(e)%20%5C))" alt="(\( P_q(e) \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20P_q(e)%20%3D%20%5Cfrac%7Bf_q(e)%7D%7BF_q%7D%0A%20%20%5C%5D" alt="\[
  P_q(e) = \frac{f_q(e)}{F_q}
  \]" />

## 3. Construct Frequency Vectors

Create vectors where each element corresponds to an entity:

- **Content Frequency Vector <img src="https://i.upmath.me/svg/(%5C(%20%5Cmathbf%7BP_c%7D%20%5C))" alt="(\( \mathbf{P_c} \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20%5Cmathbf%7BP_c%7D%20%3D%20%5BP_c(e_1)%2C%20P_c(e_2)%2C%20%5Cdots%2C%20P_c(e_n)%5D%0A%20%20%5C%5D" alt="\[
  \mathbf{P_c} = [P_c(e_1), P_c(e_2), \dots, P_c(e_n)]
  \]" />

- **Query Frequency Vector <img src="https://i.upmath.me/svg/(%5C(%20%5Cmathbf%7BP_q%7D%20%5C))" alt="(\( \mathbf{P_q} \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20%5Cmathbf%7BP_q%7D%20%3D%20%5BP_q(e_1)%2C%20P_q(e_2)%2C%20%5Cdots%2C%20P_q(e_n)%5D%0A%20%20%5C%5D" alt="\[
  \mathbf{P_q} = [P_q(e_1), P_q(e_2), \dots, P_q(e_n)]
  \]" />

**Note**: Include all unique entities from both content and queries. If an entity does not appear in one set, assign it a zero frequency in the specific set.

## 4. Compute the Alignment Score

Use **cosine similarity** to measure the alignment between the content and queries:

<img src="https://i.upmath.me/svg/%5C%5B%0A%5Ctext%7BAlignment%20Score%7D%20%3D%20%5Cfrac%7B%5Cmathbf%7BP_c%7D%20%5Ccdot%20%5Cmathbf%7BP_q%7D%7D%7B%5C%7C%5Cmathbf%7BP_c%7D%5C%7C%20%5Ctimes%20%5C%7C%5Cmathbf%7BP_q%7D%5C%7C%7D%0A%5C%5D" alt="\[
\text{Alignment Score} = \frac{\mathbf{P_c} \cdot \mathbf{P_q}}{\|\mathbf{P_c}\| \times \|\mathbf{P_q}\|}
\]" />

Where:

- **Dot Product <img src="https://i.upmath.me/svg/(%5C(%20%5Cmathbf%7BP_c%7D%20%5Ccdot%20%5Cmathbf%7BP_q%7D%20%5C))" alt="(\( \mathbf{P_c} \cdot \mathbf{P_q} \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20%5Cmathbf%7BP_c%7D%20%5Ccdot%20%5Cmathbf%7BP_q%7D%20%3D%20%5Csum_%7Be%7D%20P_c(e)%20%5Ctimes%20P_q(e)%0A%20%20%5C%5D" alt="\[
  \mathbf{P_c} \cdot \mathbf{P_q} = \sum_{e} P_c(e) \times P_q(e)
  \]" />

- **Magnitude of Vectors**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20%5C%7C%5Cmathbf%7BP_c%7D%5C%7C%20%3D%20%5Csqrt%7B%5Csum_%7Be%7D%20%5BP_c(e)%5D%5E2%7D%0A%20%20%5C%5D" alt="\[
  \|\mathbf{P_c}\| = \sqrt{\sum_{e} [P_c(e)]^2}
  \]" />
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20%5C%7C%5Cmathbf%7BP_q%7D%5C%7C%20%3D%20%5Csqrt%7B%5Csum_%7Be%7D%20%5BP_q(e)%5D%5E2%7D%0A%20%20%5C%5D" alt="\[
  \|\mathbf{P_q}\| = \sqrt{\sum_{e} [P_q(e)]^2}
  \]" />

## 5. Interpret the Alignment Score

- **Range**: The Alignment Score ranges from **0** (no alignment) to **1** (perfect alignment).
- **Higher Score**: Indicates a greater similarity between the entities in the content and the queries.

## 6. Example Calculation

### Given Data

#### Entities in Content:

| Entity         | Frequency <img src="https://i.upmath.me/svg/(%5C(%20f_c(e)%20%5C))" alt="(\( f_c(e) \))" /> |
|----------------|------------------------------|
| Company A      | 30                           |
| Location X     | 20                           |
| Commodity Y    | 50                           |

#### Entities in Queries:

| Entity         | Frequency <img src="https://i.upmath.me/svg/(%5C(%20f_q(e)%20%5C))" alt="(\( f_q(e) \))" /> |
|----------------|------------------------------|
| Company A      | 10                           |
| Location Z     | 5                            |
| Commodity Y    | 15                           |

### a. Calculate Total Frequencies

- **Total Content Frequency <img src="https://i.upmath.me/svg/(%5C(%20F_c%20%5C))" alt="(\( F_c \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20F_c%20%3D%2030%20%2B%2020%20%2B%2050%20%3D%20100%0A%20%20%5C%5D" alt="\[
  F_c = 30 + 20 + 50 = 100
  \]" />

- **Total Query Frequency <img src="https://i.upmath.me/svg/(%5C(%20F_q%20%5C))" alt="(\( F_q \))" />**:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20F_q%20%3D%2010%20%2B%205%20%2B%2015%20%3D%2030%0A%20%20%5C%5D" alt="\[
  F_q = 10 + 5 + 15 = 30
  \]" />

### b. Normalize Frequencies

#### Content Normalized Frequencies <img src="https://i.upmath.me/svg/(%5C(%20P_c(e)%20%5C))" alt="(\( P_c(e) \))" />:

- <img src="https://i.upmath.me/svg/%5C(%20P_c(%5Ctext%7BCompany%20A%7D)%20%3D%20%5Cfrac%7B30%7D%7B100%7D%20%3D%200.3%20%5C)" alt="\( P_c(\text{Company A}) = \frac{30}{100} = 0.3 \)" />
- <img src="https://i.upmath.me/svg/%5C(%20P_c(%5Ctext%7BLocation%20X%7D)%20%3D%20%5Cfrac%7B20%7D%7B100%7D%20%3D%200.2%20%5C)" alt="\( P_c(\text{Location X}) = \frac{20}{100} = 0.2 \)" />
- <img src="https://i.upmath.me/svg/%5C(%20P_c(%5Ctext%7BCommodity%20Y%7D)%20%3D%20%5Cfrac%7B50%7D%7B100%7D%20%3D%200.5%20%5C)" alt="\( P_c(\text{Commodity Y}) = \frac{50}{100} = 0.5 \)" />
- <img src="https://i.upmath.me/svg/%5C(%20P_c(%5Ctext%7BLocation%20Z%7D)%20%3D%200%20%5C)%20(since%20it%20doesn't%20appear%20in%20the%20content)" alt="\( P_c(\text{Location Z}) = 0 \) (since it doesn't appear in the content)" />

#### Query Normalized Frequencies (\( P_q(e) \)):

- <img src="https://i.upmath.me/svg/%5C(%20P_q(%5Ctext%7BCompany%20A%7D)%20%3D%20%5Cfrac%7B10%7D%7B30%7D%20%5Capprox%200.333%20%5C)" alt="\( P_q(\text{Company A}) = \frac{10}{30} \approx 0.333 \)" />
- <img src="https://i.upmath.me/svg/%5C(%20P_q(%5Ctext%7BLocation%20Z%7D)%20%3D%20%5Cfrac%7B5%7D%7B30%7D%20%5Capprox%200.167%20%5C)" alt="\( P_q(\text{Location Z}) = \frac{5}{30} \approx 0.167 \)" />
- <img src="https://i.upmath.me/svg/%5C(%20P_q(%5Ctext%7BCommodity%20Y%7D)%20%3D%20%5Cfrac%7B15%7D%7B30%7D%20%3D%200.5%20%5C)" alt="\( P_q(\text{Commodity Y}) = \frac{15}{30} = 0.5 \)" />
- <img src="https://i.upmath.me/svg/%5C(%20P_q(%5Ctext%7BLocation%20X%7D)%20%3D%200%20%5C)%20(since%20it%20doesn't%20appear%20in%20the%20queries)" alt="\( P_q(\text{Location X}) = 0 \) (since it doesn't appear in the queries)" />

### c. Construct Vectors

Include all unique entities:

- **Entities**: Company A, Location X, Person Y, Location Z

**Content Frequency Vector <img src="https://i.upmath.me/svg/(%5C(%20%5Cmathbf%7BP_c%7D%20%5C))" alt="(\( \mathbf{P_c} \))" />**:
<img src="https://i.upmath.me/svg/%5C%5B%0A%5Cmathbf%7BP_c%7D%20%3D%20%5B0.3%2C%5C%200.2%2C%5C%200.5%2C%5C%200%5D%0A%5C%5D" alt="\[
\mathbf{P_c} = [0.3,\ 0.2,\ 0.5,\ 0]
\]" />

**Query Frequency Vector <img src="https://i.upmath.me/svg/(%5C(%20%5Cmathbf%7BP_q%7D%20%5C))" alt="(\( \mathbf{P_q} \))" />**:
<img src="https://i.upmath.me/svg/%5C%5B%0A%5Cmathbf%7BP_q%7D%20%3D%20%5B0.333%2C%5C%200%2C%5C%200.5%2C%5C%200.167%5D%0A%5C%5D" alt="\[
\mathbf{P_q} = [0.333,\ 0,\ 0.5,\ 0.167]
\]" />

### d. Compute Dot Product
<img src="https://i.upmath.me/svg/%5C%5B%0A%5Cmathbf%7BP_c%7D%20%5Ccdot%20%5Cmathbf%7BP_q%7D%20%3D%20(0.3%20%5Ctimes%200.333)%20%2B%20(0.2%20%5Ctimes%200)%20%2B%20(0.5%20%5Ctimes%200.5)%20%2B%20(0%20%5Ctimes%200.167)%0A%5C%5D" alt="\[
\mathbf{P_c} \cdot \mathbf{P_q} = (0.3 \times 0.333) + (0.2 \times 0) + (0.5 \times 0.5) + (0 \times 0.167)
\]" />
<img src="https://i.upmath.me/svg/%5C%5B%0A%3D%200.0999%20%2B%200%20%2B%200.25%20%2B%200%20%3D%200.3499%0A%5C%5D" alt="\[
= 0.0999 + 0 + 0.25 + 0 = 0.3499
\]" />

### e. Compute Magnitudes

**Magnitude of Content Vector <img src="https://i.upmath.me/svg/(%5C(%20%5C%7C%5Cmathbf%7BP_c%7D%5C%7C%20%5C))" alt="(\( \|\mathbf{P_c}\| \))" />**:
<img src="https://i.upmath.me/svg/%5C%5B%0A%5C%7C%5Cmathbf%7BP_c%7D%5C%7C%20%3D%20%5Csqrt%7B(0.3)%5E2%20%2B%20(0.2)%5E2%20%2B%20(0.5)%5E2%20%2B%20(0)%5E2%7D%20%3D%20%5Csqrt%7B0.09%20%2B%200.04%20%2B%200.25%20%2B%200%7D%20%3D%20%5Csqrt%7B0.38%7D%20%5Capprox%200.6164%0A%5C%5D" alt="\[
\|\mathbf{P_c}\| = \sqrt{(0.3)^2 + (0.2)^2 + (0.5)^2 + (0)^2} = \sqrt{0.09 + 0.04 + 0.25 + 0} = \sqrt{0.38} \approx 0.6164
\]" />

**Magnitude of Query Vector <img src="https://i.upmath.me/svg/(%5C(%20%5C%7C%5Cmathbf%7BP_q%7D%5C%7C%20%5C))" alt="(\( \|\mathbf{P_q}\| \))" />**:
<img src="https://i.upmath.me/svg/%5C%5B%0A%5C%7C%5Cmathbf%7BP_q%7D%5C%7C%20%3D%20%5Csqrt%7B(0.333)%5E2%20%2B%20(0)%5E2%20%2B%20(0.5)%5E2%20%2B%20(0.167)%5E2%7D%20%3D%20%5Csqrt%7B0.1109%20%2B%200%20%2B%200.25%20%2B%200.0279%7D%20%3D%20%5Csqrt%7B0.3888%7D%20%5Capprox%200.6235%0A%5C%5D" alt="\[
\|\mathbf{P_q}\| = \sqrt{(0.333)^2 + (0)^2 + (0.5)^2 + (0.167)^2} = \sqrt{0.1109 + 0 + 0.25 + 0.0279} = \sqrt{0.3888} \approx 0.6235
\]" />

### f. Compute Alignment Score
<img src="https://i.upmath.me/svg/%5C%5B%0A%5Ctext%7BAlignment%20Score%7D%20%3D%20%5Cfrac%7B0.3499%7D%7B0.6164%20%5Ctimes%200.6235%7D%20%3D%20%5Cfrac%7B0.3499%7D%7B0.3846%7D%20%5Capprox%200.9096%0A%5C%5D" alt="\[
\text{Alignment Score} = \frac{0.3499}{0.6164 \times 0.6235} = \frac{0.3499}{0.3846} \approx 0.9096
\]" />

### g. Interpretation

An Alignment Score of approximately **0.91** indicates a high degree of alignment between the entities in your content and user queries.

## 7. Adjustments for Better Accuracy

### a. Weighting Entity Types

If certain entity types are more important, assign weights <img src="https://i.upmath.me/svg/%5C(%20w(e)%20%5C)" alt="\( w(e) \)" />:

- Modify the dot product:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20%5Cmathbf%7BP_c%7D%20%5Ccdot%20%5Cmathbf%7BP_q%7D%20%3D%20%5Csum_%7Be%7D%20w(e)%20%5Ctimes%20P_c(e)%20%5Ctimes%20P_q(e)%0A%20%20%5C%5D" alt="\[
  \mathbf{P_c} \cdot \mathbf{P_q} = \sum_{e} w(e) \times P_c(e) \times P_q(e)
  \]" />

### b. Filtering Low-Frequency Entities

- Exclude entities with frequencies below a certain threshold to reduce noise.

### c. Scaling Frequencies

- Use logarithmic scaling for large disparities in frequencies:
  <img src="https://i.upmath.me/svg/%5C%5B%0A%20%20P_c(e)%20%3D%20%5Cfrac%7B%5Clog(1%20%2B%20f_c(e))%7D%7B%5Csum_%7Be%7D%20%5Clog(1%20%2B%20f_c(e))%7D%0A%20%20%5C%5D" alt="\[
  P_c(e) = \frac{\log(1 + f_c(e))}{\sum_{e} \log(1 + f_c(e))}
  \]" />

## Conclusion

By calculating the cosine similarity between the normalized frequency vectors of entities from ICIS content and user queries, we can quantitatively measure the alignment and effectiveness of our entity recognition process. This method considers all types and frequencies of recognized entities and can be adjusted to suit specific analysis needs.

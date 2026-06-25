### FOKG - miniproject 
The point objective is to build a fact-checking engine that assigns a truth probability (0.0 to 1.0) to RDF statements.
- must train a machine learning model using provided labels to learn patterns from knowledge graphs like DBpedia.
- extracting features such as triple existence and predicate priors

## Project Requirements
Accuracy: Achieve an ROC AUC > 60% on the GERBIL evaluation platform.
Reproducibility: Code must be fully executable and documented.
Technical Standard: Use of Semantic Web technologies (RDF, SPARQL) and a standard ML approach (e.g., Logistic Regression) to model veracity.
Deadline: Final submission by July 15th, 2026.

## Thought Process
The challenge is that a triple (Subject, Predicate, Object) does not have inherent "truth." We must transform that qualitative fact into quantitative data.
- Problem: SPARQL endpoints are slow and strict. If a triple doesn't exist in the Knowledge Graph, the engine might incorrectly assume it is False (a common mistake in basic engines).
- Solution: We implement evidence blending. We query the Knowledge Graph for structural proof (Direct/Inverse matches) but back that up with statistical evidence (Predicate Priors).
- ML: By training a model on the training set, we let the computer learn the optimal "weight" of these features, rather than manually guessing how much to trust a triple match versus a statistical prior.

## Workflow
graph TD
    A[Start: Dataset Parsing] --> B[Feature Extraction]
    B --> C{SPARQL Cache?}
    C -- No --> D[Ping DBpedia]
    C -- Yes --> E[Load Local Cache]
    D --> F[Model Training]
    E --> F
    F --> G[Inference & Output]
    G --> H[GERBIL Submission]

[x] Step 1: Data Preparation

[x] Load KG-2022-train.nt

[x] Parse into Pandas DataFrame

[ ] Step 2: Feature Engineering

[ ] Calculate predicate_prior probabilities

[ ] Run GraphFeatureExtractor (with caching)

[ ] Step 3: Training

[ ] Split data into X and y

[ ] Run LogisticRegression with cross-validation

[ ] Step 4: Submission

[ ] Predict on KG-2022-test.nt

[ ] Export to result.ttl

## Libreries

```bash
pip install pandas numpy scikit-learn SPARQLWrapper requests tqdm
```

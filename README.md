# KG4CraSolver: Recommending Crash Solutions via Knowledge Graph

## Our KG

We construct a crash solution KG with 963,334 nodes and 1,626,101 edges for 245 common Java exceptions from 71,592 SO threads.

[Java exceptions types](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/KGBuilder/exception_type_set_with_size.json), the 245 common Java exceptions we parse from Java libraries from Maven Central, and extract the names of all classes that are a subclass of *java.lang.Exception* or *java.lang.Error*.

[SO threads](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/KGBuilder/all_exception_post_info.json), the related 71,592 SO threads.  we select the threads that: (1) have “java” in the title or tags, (2) have “exception” or “error” in the title or tags, (3) have an accepted answer, (4) have a positive vote for its question, and (5) contain at least one specific exception type in the given exception type list.

[Crash Solution KG](https://zenodo.org/record/7642152/files/CrashSolutionKG.V1.graph?download=1), our constructed crash solution KG with 963,334 nodes and 1,626,101 edges. 

## Benchmark

### RQ1 classification benchmark

To construct the training dataset,  we randomly select 50 Java crash-related threads (from Section 3.2) and manually annotate the sentences in these threads into the five categories.  (i.e., *Purpose*, *Symptom*, *Reason*, *Solution Step* *Others*)

[Classification training set](https://github.com/KG4CraSolver/KG4CraSolver.github.io/tree/main/Benchmark/RQ1/classification/training%20set), we separate the labeled sentences obtained from the question (i.e., *Purpose*, *Symptom*, *Others*) and those obtained from the answer (i.e., *Reason*, *Solution Step*, *Others*). As a result, we obtain 30, 133, 55, 87, and 103 sentences for *Purpose*, *Symptom*, *Reason*, *Solution Step*, and *Others* respectively.

[Classification testing set](https://github.com/KG4CraSolver/KG4CraSolver.github.io/tree/main/Benchmark/RQ1/classification/test%20set), we manually construct a benchmark of 100 crash related threads as the testing set for evaluation, which include randomly sample 100 crash-related threads that are not overlapped with the training dataset.

### RQ1 extraction benchmark

we build a training dataset for the purpose and environment phrase extraction task by further annotating the sentence classification dataset. 

[Extraction training set](https://github.com/KG4CraSolver/KG4CraSolver.github.io/tree/main/Benchmark/RQ1/extraction/training%20set),  the training set includes 120 and 616 samples for purpose phrases and environment phrases, respectively.

[Extraction testing set](https://github.com/KG4CraSolver/KG4CraSolver.github.io/tree/main/Benchmark/RQ1/extraction/test%20set), the testing set includes all purpose and symptom sentences in classification testing dataset (randomly sample 100 crash-related threads).

### RQ2 benchmark

To construct the benchmark, we first randomly select 50 exception types involved in our crash solution KG and then collect pairs of crash-related questions that 1) belong to these selected exception types; and 2) have duplicate relationships. For each exception type, we select at most 50 pairs of duplicate questions, leading to 855 pairs of duplicate questions.

[Exception types](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Benchmark/RQ2/duplicate_test_exception_type_50.json), the selected 50 exception types.

[Duplicate questions](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Benchmark/RQ2/crash_bugs_title_855.json), 855 pairs of duplicate questions.

### RQ3 benchmark

We select 12 questions describing crash bugs from the benchmark constructed in RQ2.

[Recommended result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/tree/main/Benchmark/RQ3/recommended%20result),  top-10 resolution summary of relevant posts returned by KG4CraSolver corresponding to the 12 questions.

## Result

### RQ1 result

we evaluate the effectiveness of two major steps in KG construction, i.e., crash/solution descriptive sentence classification and crash descriptive phrase extraction respectively.

we compare our classifier with a baseline that directly fine-tunes BERT with the same dataset as ours in crash/solution descriptive sentence classification, and  adopt a BERT-based sequence tagging model as the baseline to study the effectiveness of our EQA model in crash descriptive phrase extraction.

[Baseline classification result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/classification/baseline_classification_result.json), classification results of baseline on the testing set.

[Prompt classification result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/classification/prompt_classification_result.json), classification results of our method on the testing set.

[Crash/solution descriptive sentence classification evaluate result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/classification/rq1_classification_evaluate_result.json), performance of KG4CraSolver and baseline on testing dataset in crash/solution descriptive sentence classification

[Baseline purpose phrase extraction result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/extraction/baseline_purpose_extraction_result.txt),  purpose phrase extraction results of baseline on the testing set.

[Prompt purpose phrase extraction result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/extraction/prompt_purpose_extraction_result.json), purpose phrase extraction results of our method on the testing set.

[Baseline environment phrase extraction result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/extraction/baseline_environment_extraction_result.txt),  environment phrase extraction results of baseline on the testing set.

[Prompt environment phrase extraction result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/extraction/prompt_environment_extraction_result.json), environment phrase extraction results of our method on the testing set.

[Crash descriptive phrase_extraction_evaluate_result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ1/extraction/rq1_extraction_evaluate_result.json), performance of KG4CraSolver and baseline on given testing dataset in crash descriptive phrase extraction.

### RQ2 result

To evaluate the effectiveness in recommending crash solutions, we compare KG4CraSolver with baselines of two categories, i.e., existing crash solution recommendation techniques, and existing retrieval methods that recommend solutions for general questions. In particular, for the former, we include BM25-based method CraSolver; for the latter, We include word-embedding-based method AnswerBot and  sentence-embedding based method CLEAR.

[RQ2 evaluate result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ2/rq2_evaluate_result.json), performance of KG4CraSolver and all baselines on effectiveness in recommending crash solutions.

### RQ3 result

The task in this user study RQ3 is to ask participants to find solutions (i.e., SO threads) for a given crash bug with the aid of KG4CraSolver or with the baseline (i.e., using the default SO search engine).

[KG4CraSolver_result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ3/KG4CraSolver_result.json), the experimental results with the aid of KG4CraSolver.

[Baseline_result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ3/baseline_result.json), the experimental results using the default SO search engine.

We invite two extra participants with more than 4 years experience of in Java development to judge whether the returned threads provide the correct solution for the given crash. For each submitted thread, if it is judged differently by the two participants, a third participant is assigned to give an additional assessment to resolve the conflict by a majority-win strategy. 

[Final judge](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ3/ground_true_label.json), the final judge of the correct solution for 12 given crash bugs.

[RQ3_evaluate_result](https://github.com/KG4CraSolver/KG4CraSolver.github.io/blob/main/Result/RQ3/rq3_evaluate_result.json), the performance of participants to find solutions for a given crash bug with the aid of KG4CraSolver and using the default SO search engine.

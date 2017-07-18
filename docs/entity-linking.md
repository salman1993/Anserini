## Entity Linking

### Augment the freebase-subset and index it
- Use the script in "castorini/data/SimpleQuestions_v2/scripts/augment_freebase_subset.py" - [here](https://github.com/castorini/data/blob/master/SimpleQuestions_v2/scripts/augment_freebase_subset.py)
```
python augment_freebase_subset.py -f path/to/freebase -s path/to/freebase-subset -o path/to/output
```
- After augmenting the freebase-subset, gzip the file.
- Use Anserini to index the augmented gzipped freebase-subset.
```
gzip path/to/augmented-freebase-subset
```

### Create the entity linking dataset
- Download the names file from [here](https://www.dropbox.com/s/yqbesl07hsw297w/FB5M.name.txt)
- Use the script in "data/SimpleQuestions_v2/scripts/create_entity_linking_dataset.py" - [here](https://github.com/salman1993/data/blob/master/SimpleQuestions_v2/scripts/create_entity_linking_dataset.py)
```
python create_entity_linking_dataset.py -d path/to/dataset-directory -n path/to/names-file -o path/to/output
```

### Run the EntityLinking program
```
sh target/appassembler/bin/EntityLinking -index path/to/augmented/dataset -data path/to/entity-linking-dataset -hits 50 -goldData
```
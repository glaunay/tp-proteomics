```python
import re
def mitab_parser(mitab:str, uniprot_ac:list[str])->list[ list[str] ]:
    """ Extract from provided file (path), lines featurin at least one interactor 
        present in uniprot_ac provided list
        Returns: A list of mitab records split over tabulation.
    """
    hits = []
    with open(mitab, 'r') as fp:    
        for line in fp:
            line = line.split()
            for proteinfield in line[0:2]: # Test column One and Two
                _ = re.match("uniprotkb:(\\S+)", proteinfield) # Extract uniprot identifier
                x = _[1] if _ else None
                if x in uniprot_ac: # Check uniprot identifier is in provided ac list
                    hits.append(line)
                    break
                    
    print(f"Filtered {len(hits)} interactions")
    return hits

res = mitab_parser("/Users/glaunay/t.txt", ['P0A6F5', 'P02931'])
```

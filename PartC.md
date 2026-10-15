# Part C — Find alignments between Logan Search results and the query 

As presented in Part B, the Logan-Search interface enables to obtain a blast alignment between you query and the contigs or unitigs from **one** accession identifier. In case you want to perform a blast alignment between your query and **all** the contigs or unitigs from **all** or at least a subset of the accessions that were retrieved by Logan-Search, use logan_blaster.

## Instal logan_blaster
Go back to your pixi directory, and add logan_blaster:
```bash
cd ~/my_pixi_logan_env
pixi add logan_blaster
```

## Get the contigs matching the query and get the alignemnts

### Only for SRR10076195 (from partB)
Using logan blaster, how to get contigs matching the query and align the query agains these contigs?

<details><summary>Answer:</summary>
<p>

1. Create a file `accessions.txt` containing a unique line: `SRR10076195`
2. Create a file containing the queried sequence in fasta format: 

```bash
 cat query.fa 
>myquery
ATGATATTTTCAACTTTAGAGCATATATTACTTCATATATCCTTTTCGGTGGTTTCAATTGTAATTACAATTCAATTGATAACCTTGTTAGTCGATGAAATCATAGGACTATGTGATTCATCCGAAAAAGGGATGGTAGCGACTTTTTGCTGTATAACAGGATTATTAGTTACTCGTTGGATTTATTGGGGACATTTACCATTAAGTAATTTATATGAATCATTAATCTTTCTTTCATGGAGTTTCTCCATTATTTATATGGTTCCACTTTTTAAAAAATATAAAAACTATTTCAATGTAAACGTAATAACCGCGCCGAGTGTTAATTTTACCCAAGGTTTTGCTACTTCGGGTCTTTTAAATGAAATGAATCAATCCGAAATATTAGTACCCGCTCTTCAATCCCATTGGTTAATGATGCACGTAAGTATGATGGTATTGAGCTATGCAGCTCTTTTATGCGGATCATTATTATCACTAGCTCTTCTAGTCATTACATTTCGAAAATTCATAAGAATTCTTAGTCAAAGTAATAATTTAGTAAATGAGTCTTTTTCTTGGAGCGAGATTGAATACGTGAGAGAAAAAAAAAATATTTTACAAAAGACTTCTTTTCTTTCTTCTAGGAATTATTACAGGTTTCAATTGGTTCAACAATTGGATCTTTGGAGTTATCGTATTATTAGTCTAGGGTTTACCTTTTTAACCATAGGTATTCTTTCAGGCGCAGTATGGGCTAATGAAGCATGGGGATCCTATTGGAATTGGGATCCAAAGGAGACTTGGGCATTTATTACTTGGACCATATTTGCCATTTATTTACATACTAGAACAAATAAAAATTTTGAAAGCGTAAATTCCGCAATTGTAGCCTCGATAGGCTTTCTTATAATTTGGGTATGCTATTTTGGGGTTAATTTATTAGGAATAGGGTTGCATAGTTATGGTTTATTTCCTAATTGA
```

3. logan_blaster:

```bash
logan_blaster -a accession.txt -q query.fa 
```

- Downloaded data are in `query_1/logan_data/SRR10076195.contigs.fa.zst` 
- Contigs with a hit with the query are in `query_1/logan_data/SRR10076195.recruited_contigs.fa`
- Alignments are in `query_1/alignments/myquery_vs_SRR10076195.txt`
- Synthesis of the alignment are in `query_1/alignments/synth_myquery_vs_SRR10076195.txt`

</p>
</details>

## Get the unitigs matching the query and get the alignemnts
Using logan blaster, how to get **unitigs** matching the query and align the query agains these **unitigs**?

<details><summary>Answer:</summary>
<p>

Same command with the `-u` option: `logan_blaster -a accession.txt -q query.fa -u`

</p>
</details>


Results will appear in the `query_2` directory.

## Automatize the download & alignement to (all) matched accessions:

In order to get the unitigs/contigs of all matched accessions, just run 

```bash
logan_blaster -s <session_name>
```

Results will be stored in directory `session_session_name`.

<details><summary>For example:</summary>
<p>

```bash
 logan_blaster -s kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4 --limit 2
```
(for the purpose of this tuto, we limit the analysis to the two best hits).

Results will be stored in directory `session_kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4/`.
</p>
</details>

---

Explain the logs eg: 
```bash
[INFO] Coverage statistics for downloaded contigs (ERR1727496):
  Number of sequences:          127384
  Total length:                 39615525 bp
  Mean coverage:                12.596
  Median coverage (sequences):  3.700
  Median coverage (bases):      4.600
```

and

```bash
[INFO] Coverage statistics for recruited contigs (ERR1727496):
  Number of sequences:          21
  Total length:                 46664 bp
  Mean coverage:                36.983
  Median coverage (sequences):  8.503
  Median coverage (bases):      41.537
```

---
Where are the dowloaded sequences?

<details><summary>Answer:</summary>
<p>

In `session_kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4/logan_data/*.contigs.fa.zst `
</p>
</details>

---

Where are the dowloaded contigs among sequences, sharing similarity with the query?


<details><summary>Answer:</summary>
<p>

In `session_kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4/logan_data/*.recruited_contigs.fa.zst `
</p>
</details>

The recruited format is explained in this example

```
>DRR024392_74826 ka:f:61.428   L:-:4702013:-  L:+:1198012:-  2 0.20429

"DRR024392_74826" accession_id 
"ka:f:61.428" coverage (orginal data)
"L:-:4702013:-  L:+:1198012:-" graph links
    L:side:target:orientation
"2" number of kmers exactly shared with the query (k being given as a parameter to logan_blaster)
"0.20429"
```

--- 

Where are the alignements?
<details><summary>Answer:</summary>
<p>

In `session_kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4/alignments/<myqueryname>_vs_ERR011184.txt`
</p>
</details>

--- 

Where are the synthese of alignments?
<details><summary>Answer:</summary>
<p>

In `session_kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4/alignments/synth_<myqueryname>_vs_ERR011184.txt`
</p>
</details>

---
How to interpret such a synthesis?

<details><summary>Answer:</summary>
<p>
Check https://github.com/pierrepeterlongo/logan_blaster/blob/main/README.md#synthesis-of-the-alignments
</p>
</details>


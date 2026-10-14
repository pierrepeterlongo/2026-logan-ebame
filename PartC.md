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
 logan_blaster -s kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4
```

Results will be stored in directory `session_kmviz-731f1aed-4c45-4473-a08a-5a6dafa3adc4/`.
</p>
</details>

# HSE_minor_project_23

Создаем файл drosophila.blast с последовательностью [отсюда](https://genome.ucsc.edu/cgi-bin/hgGene?hgsid=1642477790_R4rptSoOdAkvf2a3AR4gZJd1VK2j&hgg_do_getProteinSeq=1&hgg_gene=ENST00000266775.13).

Запускаем поиск BLASTp белка TDG против 11-ти протеомов.
Делаем это с помощью bash скрипта:

```
declare -a StringArray=("human" "mouse" "zebrafish" "drosophila" "c.elegans" "ciliate" "yeast" "methanocaldococcus" "thermococcus" "e.coli" "tuberculosis")

for i in ${StringArray[@]}; do
    echo $i
    blastp  -query tdg.fasta  -db /mnt/storage/project_2023/proteomes/$i.faa  -out $i.blast  -outfmt 7
done
```

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
Добавляем все полученные результаты в архив и скачиваем его с сервера:

```
zip -R first_blast '*.blast'
```
В другом терминале запускаем команду скачивания:
```
scp -i /Users/lizashcherbakova/.ssh/id_rsa -P 32222 eascherbakova_2@89.175.46.92:/home/eascherbakova_2/project/first_blast.zip /Users/lizashcherbakova/hse/bioinfa/project/blast1
```
*Проделываем аналогичную операцию для гистонов.*

Создаем новую папку для определенного гистона.
Записываем туда его fasta файл.
Копируем скрипт.
```
mkdir h2a
touch h2a.fasta
cp ../blast1.sh blast_h2a.sh
```
Меняем внутри него tdg.fasta на <название гистона>.fasta.

Запускаем скрипт
Архивируем результаты.
```
bash blast_h2a.sh 
zip -R h2a_blast '*.blast'
```
Скачиваем на локальный компьютер.
```
scp -i /Users/lizashcherbakova/.ssh/id_rsa -P 32222 eascherbakova_2@89.175.46.92:/home/eascherbakova_2/project/h2a/h2a_blast.zip /Users/lizashcherbakova/hse/bioinfa/project/blast1
```

# lab-notebook
lab notebook for gen 711
mkdir trimmed_fastqs
conda activate genomics
git clone https://github.com/MacCarey03/Gen711_Final_Cyano.git
cd Gen771_Final_Cyano
git add testfile.txt
get committ
get push
Three above did not work because of premission issues
cp /tmp/gen711_project_data/fastp.sh <path to github directory>/fastp.sh
chmod +x <path to github directory>/fastp.sh
problems with gethub directory, used ~ for home directory
cp /tmp/gen711_project_data/fastp.sh ~/fastp.sh
chmod +x ~/fastp.sh
<path to github directory>/fastp.sh <1.poly-g length> <1.path to fastq directory>  <3.path to your output directory>
./fastp.sh 150 /tmp/gen711_project_data/cyano/fastqs trimmed_fastqs
after it has finished
conda activate qiime2-2022.8 

AFTER THIS POINT, COMMANDS STOPPED WORKING

qiime tools import --type "SampleData[PairedEndSequencesWithQuality]" --input-path fastp.sh  --output-path trimmed_fastqs
qiime cutadapt trim-paired --i-demultiplexed-sequences trimmed_fastqs --p-cores 4 --p-front-f GTGYCAGCMGCCGCGGTAA --p-front-r CCGYCAATTYMTTTRAGTTT --p-discard-untrimmed --p-match-adapter-wildcards --verbose --o-trimmed-sequences trimmed_fastqs/trimmedcyano.qza
qiime demux summarize --i-data trimmed_fastqs --o-visualization trimmed_fastqs/trimmedcyano.qzv
qiime dada2 denoise-paired --i-demultiplexed-seqs qiime_out/${run}_demux_cutadapt.qza --p-trunc-len-f ${trunclenf} --p-trunc-len-r ${trunclenr} --p-trim-left-f 0 --p-trim-left-r 0 --p-n-threads 4 --o-denoising-stats trimmed_fastqs/denoising-stats.qza --o-table trimmed_fastqs/feature_table.qza --o-representative-sequences trimmed_fastqs/rep-seqs.qza
qiime metadata tabulate --m-input-file trimmed_fastqs/denoising-stats.qza --o-visualization trimmed_fastqs/denoising-stats.qzv 
qiime feature-table tabulate-seqs --i-data trimmed_fastqs/rep-seqs.qza --o-visualization trimmed_fastqs/rep-seqs.qzv

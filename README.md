##################
# allelecount.py #
##################

SNP counter script written for parsing samtools mpileup output (v0.1.19).

Written by Nathaniel Lim (May 2014) for Joshua Mell and Rosie Redfield.

Written for Python 3.4. Works with Python 3.3.1.  Does not work with Python 2.x.

Intended to take samtools mpileup output (v0.1.19) from a single BAM file from STDIN and gives count columns to STDOUT

Recommended usage: samtools mpileup -ABE -d 100000 -q1 reads.ref.bam | allelecount.py | gzip > reads.ref.counts.txt.gz

Use with samtools mpileup WITHOUT indicating a reference sequence (no -f option)

Upfront filtering can use samtools view or sambamba view for finer control of what reads/bases get counted.  
Use of -q 1 option excludes multiply mapping reads, if using bwa mem alignments


Output columns are tab-delimited: 

chr pos A C G T N a c g t n IN DEL indel

The first two columns, chr and pos, are as indicated by the bam.  Note, only positions present in the bam are reported.

The next 12 columns specify counts of each base (including N) on each strand, as well as a count of insertions (INS) that follow the specified base and deletions (DEL) that include the specified base.

Final indel field (column 15) is only written for positions that indels were detected (i.e. leaves last column ragged). This field specifies counts of each insertion detected following the position and each deletion including the position.

Revised on 2014-05-15 (rev 3).  Revised again on 2016-03-14 (rev 4) to re-order ATCGN to ACGTN.

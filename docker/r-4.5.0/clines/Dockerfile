FROM --platform=linux/arm64 rocker/r-ver:4.5.0

# Install system dependencies
RUN apt-get update && apt-get install -y \
    zlib1g-dev \
    libhts-dev \
    libbz2-dev \
    libssl-dev \
    libpng-dev \
    libxml2-dev

# Configure readline history search
RUN echo '"\e[A":history-search-backward' >> /root/.inputrc && \
    echo '"\e[B":history-search-forward' >> /root/.inputrc && \
    echo '"\e.":yank-last-arg' >> /root/.inputrc

# Install R packages
RUN Rscript -e 'install.packages(c("BiocManager", "ggplot2", "readr", "dplyr", "cowplot", "RColorBrewer", "tidyr", "ggsignif", "pheatmap", "ashr", "pheatmap"))'

# Install Bioconductor 3.21
RUN Rscript -e 'BiocManager::install(version = "3.21")'
RUN Rscript -e 'BiocManager::install(c("tximport", "DESeq2", "IHW", "GOstats", "GSEABase"))'

# Set working directory
WORKDIR /data

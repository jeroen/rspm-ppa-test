FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive

RUN \
    apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:marutter/rrutter4.0 && \
    apt-get update && \
    apt-get install -y git curl pandoc pandoc-citeproc r-base-dev libcurl4-gnutls-dev \
    libgit2-dev libpoppler-cpp-dev libtesseract-dev libleptonica-dev tesseract-ocr-eng libmagick++-dev

RUN RPROFILE=$(R RHOME)/etc/Rprofile.site && \
    echo 'options(repos = c(CRAN = "https://packagemanager.rstudio.com/all/__linux__/xenial/latest"))' >> "$RPROFILE" && \
    echo 'options(HTTPUserAgent = sprintf("R/%s R (%s)", getRversion(), paste(getRversion(), R.version$platform, R.version$arch, R.version$os)))' >> "$RPROFILE"

RUN R -e 'install.packages(c("magick", "tesseract", "pdftools"))'

RUN R -e 'lapply(c("magick", "tesseract", "pdftools"), require, character.only=T)'

RUN \
    add-apt-repository -y "ppa:cran/travis" && \
    apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get autoremove -y --purge

RUN R -e 'lapply(c("magick", "tesseract", "pdftools"), require, character.only=T)'

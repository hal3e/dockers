FROM alpine:latest

RUN mkdir /tmp/install-texlive

WORKDIR /tmp/install-texlive

# Install TeX Live
RUN apk --no-cache add perl wget xz tar && \
	wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
	tar --strip-components=1 -xvf install-tl-unx.tar.gz && \
  echo "selected_scheme scheme-minimal" >> texlive.profile && \
  ./install-tl --profile=texlive.profile && \
  apk del perl wget xz tar && \
	cd / && rm -rf /tmp/install-texlive

ENV PATH="/usr/local/texlive/2022/bin/x86_64-linuxmusl:${PATH}"

# Install basic collection and additional packages
RUN apk --no-cache add perl wget fontconfig && \
  tlmgr install latex-bin xetex sourcesanspro enumitem xifthen ifmtarg \
  tcolorbox environ tools ragged2e geometry fancyhdr xcolor etoolbox \
  setspace fontspec unicode-math amsmath xkeyval pgf parskip kvoptions \
  ltxcmds kvsetkeys hyperref infwarerr && \
  apk del perl wget && \
	mkdir /workdir

WORKDIR /workdir

VOLUME ["/workdir"]

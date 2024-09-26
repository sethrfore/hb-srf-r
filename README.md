# Customizable R formula for Homebrew

This is a custom Homebrew R formula that enables OpenBLAS and OpenMP for accelerated linear algebra. It does not require X11/XQuartz and instead relies on Cairo for graphics support. It includes dependencies listed in [this blog post](https://www.btskinner.io/code/install-r-with-openblas-and-openmp-on-macos-mojave/) by Benjamin T. Skinner.

On macOS, you must first install XCode Command Line Tools, but this should be installed with Homebrew. Seth Fore's version also includes Tcl-Tk by default, but we do not require it. There is also optional support for IUC, Java, Pango, and TexInfo, but none of these are strictly required.

# Installation

This modified R formula can be installed as follows.

Add the repository to your homebrew
```sh
brew tap cole-trapnell-lab/homebrew-r-srf
```

Check available installation options

```sh
brew info cole-trapnell-lab/r-srf/r
```

Compile the modified R formula:

```sh
brew install cole-trapnell-lab/r-srf/r
```

You should also install the `cmake` cask so you can install some R packages:

```sh
brew install --cask cmake
```

Check if the default R is correct by running `which R`. It should be `$(brew --prefix)/bin/R`, e.g. `/opt/homebrew/bin/R`. You might have to start a new terminal session for it to take effect.

Note: If necessary, remove previous R and cairo installations prior to compiling the modified R formula. Once installed, the compiled dependencies can be checked by invoking R and running `capabilities()`. You can test if everything is as expected with the following:
```r
all(capabilities == c(jpeg = TRUE,
					  png = TRUE,
					  tiff = TRUE,
					  tcltk = FALSE,
					  X11 = FALSE,
					  aqua = TRUE,
					  `http/ftp` = TRUE,
					  sockets = TRUE,
					  libxml = FALSE,
					  fifo = TRUE,
					  cledit = TRUE,
					  iconv = TRUE,
					  NLS = TRUE,
					  Rprof = TRUE,
					  profmem = TRUE,
					  cairo = TRUE,
					  ICU = TRUE,
					  long.double = FALSE,
					  libcurl = TRUE)
)
```

If the result of the above is not TRUE, check the individual `capabilities()`:
```r
       jpeg         png        tiff       tcltk         X11        aqua
       TRUE        TRUE        TRUE       FALSE       FALSE        TRUE
   http/ftp     sockets      libxml        fifo      cledit       iconv
       TRUE        TRUE       FALSE        TRUE        TRUE        TRUE
        NLS       Rprof     profmem       cairo         ICU long.double
       TRUE        TRUE        TRUE        TRUE        TRUE       FALSE
    libcurl
       TRUE
```

# R/X11 support deprectation notice

While I won't be immediately deprecating X11 supported R builds, I am currently unlikely to continue maintaining them at some point in the future. For those affected by this, please refer and post any comments to this [discussion thread](https://github.com/sethrfore/homebrew-r-srf/discussions/40). All notices pertaining changes to R/X11 support will be posted here or in the relevant discussion. If you have any thoughts, suggestions or concerns surrounding how/when this process will take place, I highly recommend contributing to the discussion. 

# Note for R Developers

I am open to suggestions on how to improve the functionality of this formula. I am not a programming expert and welcome any tested solutions that enhance the functionality of this formula, specifically with reference to issues related to changes in recent Xcode and CLT deployments.

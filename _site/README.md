# Murata Laboratory

We are a research group in Department of Computer Science, 
School of Computing, Tokyo Institute of Technology.
This website is a place to accumulate our common knowledge and paper
reading list. 

**Any information or opinion on this website
(net-titech.github.io) belongs to individual members of the laboratory
alone, hence it does not represent the view of Murata Laboratory,
Department of Computer Science, School of Computing, nor Tokyo Institute 
of Technology.**

# Leonids Jekyll Themes

We use Leonids theme for this website: **[Leonids](http://renyuanz.github.io/leonids)**.

## What is Leonids?

* Responsive templates. Looking good on mobile, tablet, and desktop.
* Simple and clear permalink structure.
* Support for Disqus Comments.
* Support for multi-authors.
* **And** the Leonids (/ˈliːənɪdz/ lee-ə-nidz) are a prolific meteor shower associated with the comet [Tempel-Tuttle](https://en.wikipedia.org/wiki/55P/Tempel%E2%80%93Tuttle).

See a [demo](http://renyuanz.github.io/leonids/) hosted on GitHub.

## Quick setup

```
git clone https://github.com/renyuanz/leonids
cd leonids
jekyll server
```

Check out your awesome blog at `http://localhost:4000` and Cheers!

## Running with Docker

```
docker run --rm -it --volume=$PWD:/srv/jekyll -p 4000:4000 jekyll/jekyll:pages jekyll serve --watch --force_polling
```

# RFC: Packages as Optional Namespaces
 
This is a separate RFC repo for discussing the "Packages as Optional Namespaces" RFC for crates.io.

This was previously a pre-RFC at https://internals.rust-lang.org/t/pre-rfc-packages-as-optional-namespaces/13059.


You can read the text [here](https://github.com/Manishearth/namespacing-rfc/blob/main/0000-packages-as-optional-namespaces.md).

**There is now a prototype that you can try out [here](https://github.com/Manishearth/namespacing-rfc/issues/10)**

## Background

There have been a _lot_ of discussions about namespacing in cargo. (most recently: https://internals.rust-lang.org/t/pre-rfc-hyper-minimalist-namespaces-on-crates-io/13041 and https://internals.rust-lang.org/t/pre-rfc-user-namespaces-on-crates-io/12851).

There are some strong opinions about this floating around. From my perspective, most of the tension around this is that people have different sets of problems they want solved, some people want to solve squatting, some people want to solve ownership. The many years of talking past each other has left a lot of people feeling unheard and hurt.

I've been quietly talking to people, one-on-one, about this for _years_, to try and get an idea of how best to move forward here. I've had conversations with crates.io and cargo team members, as well as with community members, to better understand the space. I have presented various forms of this proposal to them and received positive responses. I do think this is a viable and good path forward, but for this to work out we need to be our best selves here.

I would like to request everyone to keep this discussion  constructive and respectful.


This proposal is similar to https://internals.rust-lang.org/t/pre-rfc-packages-as-namespaces/8628 , but a bit more fleshed out.

This is not an official proposal from any relevant team. While I have discussed this with teams at various points, I have largely been an interested outsider to this whole set of discussions. After seeing discussions get rehashed again and again, I felt it is worth putting this proposal out there to maybe try and make progress this long standing issue.

## Scope

As mentioned before, there are many different problems people want namespacing to solve. Here are a couple I've seen over the course of my discussions:

 - Namespacing to indicate organization ownership -- e.g. knowing that `regex/foo` is a crate you can trust if you trust `regex`.
 - Namespacing as a way to prevent squatting -- everyone publishes under `username/foo` or `org/foo` and thus names cannot overlap
 - Namespacing as a way to talk about multi-crate "packages" -- e.g. having a `serde` "package" that contains simul-versioned `serde` and `serde/derive` crates.

The focus of this proposal is the first problem only.

I do not find namespacing to be a solution to the problem of general squatting, for reasons that have been articulated many times (I don't want to go into it here, but feel free to DM me if you want to know more).


As for the multi-crate "package" concept, I'm interested in that kind of thing being possible but I feel like that does not need namespaces to work. There are some community members working on proposals in that space too.

Anyway, I'd like to keep the discussion here focused on the first problem _only_. The other problems are worth discussing, but let's please stay on topic!

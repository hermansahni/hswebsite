---
title: JAD2020
summary: Institutional Quality, Infrastructure and Economic Growth in Africa
authors:
- admin
- Christian Nsiah
- Bichaka Fayissa
tags:
- Infrastructure
- Governance
- Rule of Law
- ICT
- Transport
- Electricity
- Water and Sanitation
- Economic Growth
- Africa
- World Bank
- Fixed effects
- Threshold Analysis
- System GMM estimation
- Panel data
- Allied Social Sciences Associations
- Journal of African Development
- 2020
- JEL H54
- JEL O40
- JEL O43
- JEL O47
- JEL O55
categories: []
date: "2019-02-05T00:00:00Z"
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  theme: black
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  highlight_style: dracula
---

## Institutional Quality, Infrastructure and Economic Growth in Africa

### Herman Sahni, Christian Nsiah, Bichaka Fayissa

[African Finance & Economics Association]() | [Allied Social Sciences Association 2020]()


---

### Outline

- Motivation and objectives of the Paper
- Literature review & contributions
- The Empirical Models
- Summary and Interpretations of Results
- Conclusions and Policy Implications

---

### Outline



```graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

---


#### Literature

Infrastructure Quality Index

_Ranking_

- No African country in the top 20
- Highest ranked:
-- Rwanda (40), Seychelles (41), Morocco (42), Namibia (45), Mauritius (50)
- 14 African countries ranked in the bottom 20
- Source: [reports.weforum.org/global-competitiveness-index-2017-2018/](https://reports.weforum.org/global-competitiveness-index-2017-2018/)

---

#### Literature (cont'd.)

Infrastructure Quality Index

_Electricity Issues_

- Frequent power outages, restricting access to electricity to a third of Africa’s
population, reducing its productivity by as much as 40%, and curtailing its
annual economic growth by about 2% ([PIDA, 2014](https://www.afdb.org/en/topics-and-sectors/initiatives-partnerships/programme-for-infrastructure-development-in-africa-pida))
- Only 30% of African countries have access to electricity relative to 70%-90% of other developing countries 

---

#### Motivation 

Infrastructure & Growth

* Well-designed infrastructure investments (Energy, transport, digital communications, waste disposal networks, and water and sanitation facilities) have long-term economic benefits
    * Infrastructure raise productivity, decrease transportation and communication costs, increase land values, improve health
    * Cause significant positive spillovers.

---

#### Motivation (cont'd.)

Infrastructure & Growth

* However, investing wisely in infrastructure is critically important
    * Over-investment can lead to inefficiency and low marginal returns

---

#### Link between Infrastructure and Growth 

* Channels through which infrastructure impacts growth
    * direct input into the production process
    * complement to other inputs into the production process
    * stimulant to factor accumulation by providing facilities for human development
    * tool to guide industrial policy ([Wolassa, 2012](https://ideas.repec.org/p/adb/adbwps/438.html)). 


















## Outline

- Efficiently write slides in Markdown
- 3-in-1: Create, Present, and Publish your slides
- Supports speaker notes
- Mobile friendly slides

---

## Controls

- Next: `Right Arrow` or `Space`
- Previous: `Left Arrow`
- Start: `Home`
- Finish: `End`
- Overview: `Esc`
- Speaker notes: `S`
- Fullscreen: `F`
- Zoom: `Alt + Click`
- [PDF Export](https://github.com/hakimel/reveal.js#pdf-export): `E`

---

## Code Highlighting

Inline code: `variable`

Code block:
```python
porridge = "blueberry"
if porridge == "blueberry":
    print("Eating...")
```

---

## Math

In-line math: $x + y = z$

Block math:

$$
f\left( x \right) = \;\frac{{2\left( {x + 4} \right)\left( {x - 4} \right)}}{{\left( {x + 4} \right)\left( {x + 1} \right)}}
$$

---

## Fragments

Make content appear incrementally

```
{{%/* fragment */%}} One {{%/* /fragment */%}}
{{%/* fragment */%}} **Two** {{%/* /fragment */%}}
{{%/* fragment */%}} Three {{%/* /fragment */%}}
```

Press `Space` to play!

{{% fragment %}} One {{% /fragment %}}
{{% fragment %}} **Two** {{% /fragment %}}
{{% fragment %}} Three {{% /fragment %}}

---

A fragment can accept two optional parameters:

- `class`: use a custom style (requires definition in custom CSS)
- `weight`: sets the order in which a fragment appears

---

## Speaker Notes

Add speaker notes to your presentation

```markdown
{{%/* speaker_note */%}}
- Only the speaker can read these notes
- Press `S` key to view
{{%/* /speaker_note */%}}
```

Press the `S` key to view the speaker notes!

{{< speaker_note >}}
- Only the speaker can read these notes
- Press `S` key to view
{{< /speaker_note >}}

---

## Themes

- black: Black background, white text, blue links (default)
- white: White background, black text, blue links
- league: Gray background, white text, blue links
- beige: Beige background, dark text, brown links
- sky: Blue background, thin dark text, blue links

---

- night: Black background, thick white text, orange links
- serif: Cappuccino background, gray text, brown links
- simple: White background, black text, blue links
- solarized: Cream-colored background, dark green text, blue links

---

{{< slide background-image="/media/boards.jpg" >}}

## Custom Slide

Customize the slide style and background

```markdown
{{</* slide background-image="/media/boards.jpg" */>}}
{{</* slide background-color="#0000FF" */>}}
{{</* slide class="my-style" */>}}
```

---

## Custom CSS Example

Let's make headers navy colored.

Create `assets/css/reveal_custom.css` with:

```css
.reveal section h1,
.reveal section h2,
.reveal section h3 {
  color: navy;
}
```

---

# Questions?

[Ask](https://spectrum.chat/academic)

[Documentation](https://sourcethemes.com/academic/docs/managing-content/#create-slides)

{{ $mermaid := resources.Get "/path/to/mermaid.min.js" }}
<script src="{{ $mermaid.RelPermalink }}"></script>
<script>
    window.onload = function() {
        mermaid.init(undefined, ".language-mermaid");
    };
</script>


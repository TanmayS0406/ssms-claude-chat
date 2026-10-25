---
layout: default
title: SSMS Claude Chat security report
permalink: /security/
description: Live security report for SSMS Claude Chat. Every change and every day, the code and installer are scanned for security bugs, leaked secrets, vulnerable libraries and viruses.
---

# SSMS Claude Chat security report

SSMS Claude Chat is checked by more than a dozen well-known security tools every time the code changes, and again
every day, because new problems are discovered all the time. This page shows the latest results, updated
automatically after each scan.

{% assign r = site.data.security %}
{% if r %}

<img class="sec-banner" src="{{ '/security/banner.svg' | relative_url }}?v={{ r.generated | date: '%s' }}" alt="SSMS Claude Chat security scan: {% if r.status == 'pass' %}all security checks passed{% else %}some checks need attention{% endif %}, last scan {{ r.generated | date: '%-d %B %Y' }}">

<div class="sec-summary sec-{{ r.status }}">
  <div class="sec-big">{% if r.status == 'pass' %}✅ All security checks passed{% else %}⚠️ Some checks need attention{% endif %}</div>
  <div>Last scan: <strong>{{ r.generated | date: "%-d %B %Y, %H:%M UTC" }}</strong>{% if r.release and r.release != '' %} · Latest release: <strong>{{ r.release }}</strong>{% endif %} · Code version: <code>{{ r.commit }}</code></div>
</div>

<table class="sec-table">
  <thead><tr><th>Check</th><th>What it looks for</th><th>Result</th><th>Findings</th></tr></thead>
  <tbody>
  {% for c in r.checks %}
    <tr>
      <td><strong>{{ c.name }}</strong><br><span class="sec-tools">{{ c.tools }}</span></td>
      <td>{{ c.about }}{% if c.note %}<br><span class="sec-note">{{ c.note }}</span>{% endif %}</td>
      <td class="sec-result">
        {% case c.result %}
          {% when 'pass' %}<span class="pill pill-pass">✓ Passed</span>
          {% when 'fail' %}<span class="pill pill-fail">✗ Failed</span>
          {% when 'cancelled' %}<span class="pill pill-fail">Interrupted</span>
          {% else %}<span class="pill pill-skip">Not run</span>
        {% endcase %}
      </td>
      <td class="sec-findings">
        {% if c.findings %}
          {% assign total = c.findings.critical | plus: c.findings.high | plus: c.findings.medium | plus: c.findings.low %}
          {% if total == 0 %}None{% else %}
            {% if c.findings.critical > 0 %}<span class="sev sev-critical">{{ c.findings.critical }} critical</span> {% endif %}
            {% if c.findings.high > 0 %}<span class="sev sev-high">{{ c.findings.high }} high</span> {% endif %}
            {% if c.findings.medium > 0 %}<span class="sev sev-medium">{{ c.findings.medium }} medium</span> {% endif %}
            {% if c.findings.low > 0 %}<span class="sev sev-low">{{ c.findings.low }} low</span>{% endif %}
          {% endif %}
        {% elsif c.result == 'pass' %}None{% else %}–{% endif %}
      </td>
    </tr>
  {% endfor %}
  </tbody>
</table>

{% if r.signed %}
**Signed installer:** the setup file is digitally signed, so Windows can confirm it really comes from us and hasn't
been changed.
{% else %}
**Signed installer:** not yet. Code signing is being set up; until then Windows may show a "Windows protected your
PC" message when you run the setup.
{% endif %}

{% else %}
The first report will appear here after the next scan.
{% endif %}

## What the results mean

- **Passed** means the check found nothing at or above the level we treat as unacceptable. Smaller findings are
  still counted and reviewed.
- **Findings** are counted, but the details are not published here. That way nobody can learn about a problem
  before it is fixed.
- **Vulnerable libraries** also counts libraries that are only used to *build* SSMS Claude Chat and are not inside
  the installer. The **Installer scan** checks exactly what you download.

## What's inside the installer

The installer scan also produces a full list of what's inside the download (a "software bill of materials"):
[sbom.spdx.json]({{ '/security/sbom.spdx.json' | relative_url }}).

## How SSMS Claude Chat keeps you safe

- **Nothing changes in your database without your OK.** You see the exact SQL and where it will run, then click
  Yes or No. You can also switch changes off completely.
- **Looking is read-only.** When Claude reads data to answer a question, it can't write, and every query is undone
  afterwards.
- **Your Claude password is never seen.** You sign in to Claude in your browser.
- **Your data stays on your computer**, apart from what is sent to Claude to answer you. See the
  [FAQ](../faq/#what-does-claude-see).
- **Claude can only do what your SQL Server login allows.**

## Found a security problem?

Please tell us privately rather than in a public issue: see [how to report a vulnerability]({{ site.repository_url }}/security/policy).

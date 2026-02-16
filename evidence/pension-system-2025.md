---
layout: page
title: "EV-001 年金システム 明細作成処理改修・移行"
permalink: /evidence/pension-system-2025/
---

<div class="modern-page evidence-detail">
  <section class="modern-hero">
    <p class="hero-eyebrow">EV-001</p>
    <h1 class="hero-title">年金システム 明細作成処理改修・移行</h1>
    <p class="hero-subtitle">明細作成処理と移行対応を中心に、設計〜テストまでを担当。</p>
    <div class="nav-pills">
      <a href="/evidence/">Evidence一覧</a>
      <a href="/dashboard/">Dashboard</a>
      <a href="/skills/">Skills</a>
    </div>
  </section>

  <section>
    <h2>期間</h2>
    <p>2025-07 〜 2026-02（継続）</p>
  </section>

  <section>
    <h2>役割</h2>
    <p>メンバー（14名体制）</p>
  </section>

  <section>
    <h2>担当</h2>
    <ul class="list-tight">
      <li>明細作成処理の改修</li>
      <li>新システム移行向けの月次処理修正</li>
      <li>基本設計、詳細設計、実装、試験（結合/総合）</li>
    </ul>
  </section>

  <section>
    <h2>技術</h2>
    <p><span class="tag">Java</span><span class="tag">Oracle</span><span class="tag">JP1</span><span class="tag">Linux</span><span class="tag">Windows</span></p>
  </section>

  <section>
    <h2>成果</h2>
    <ul class="list-tight">
      <li>既存月次処理を新システム仕様に合わせて改修</li>
      <li>設計〜テストまで一気通貫で担当し、移行フェーズの品質を維持</li>
      <li>試験工程での不整合を早期に検出し、手戻りを低減</li>
    </ul>
  </section>

  <section>
    <h2>学び</h2>
    <ul class="list-tight">
      <li>バッチ/ジョブ連携を含む改修は、テスト観点を初期設計時に定義するほど安定する</li>
      <li>OS混在環境ではログ出力粒度を揃えると障害切り分けが速くなる</li>
    </ul>
  </section>

  <section>
    <h2>再現ポイント（運用/品質）</h2>
    <ul class="list-tight">
      <li>変更点ごとに「入力・変換・出力」の確認観点を固定化してレビューする</li>
      <li>JP1ジョブ異常時の一次切り分け手順（ログ確認順）を事前にRunbook化する</li>
      <li>結合テスト前にSQL/ジョブ/アプリの責務境界を明文化する</li>
    </ul>
  </section>
</div>

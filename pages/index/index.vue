<template>
  <view class="page">
    <view class="hero">
      <view class="badge"><view class="badge-dot"></view><text>你的 AI 协作助手</text></view>
      <text class="headline">把想法，<text>变成结果</text></text>
      <text class="intro">从灵感、文案到代码与数据分析，我能陪你把每一步做得更清晰、更轻松。</text>
      <button class="primary-button" @click="startChat">开始一段对话 <text>→</text></button>
      <text class="hint">随时提问，无需准备</text>
    </view>

    <view class="section-head">
      <text class="kicker">我能帮你做什么</text>
      <text class="section-title">一位多面手，专注你的目标</text>
    </view>
    <view class="cards">
      <view v-for="item in capabilities" :key="item.title" class="card">
        <view class="icon" :class="item.color"><text>{{ item.icon }}</text></view>
        <view class="card-copy"><text class="card-title">{{ item.title }}</text><text class="card-desc">{{ item.description }}</text></view>
        <text class="chevron">›</text>
      </view>
    </view>

    <view class="workflow">
      <view class="workflow-head"><view><text class="kicker">简单三步</text><text class="workflow-title">从问题到答案</text></view><text class="sparkle">✦</text></view>
      <view v-for="(step, index) in steps" :key="step.title" class="step">
        <text class="step-no">0{{ index + 1 }}</text>
        <view><text class="step-title">{{ step.title }}</text><text class="step-desc">{{ step.description }}</text></view>
      </view>
    </view>
    <view class="footer"><text>Built for curious minds</text><view></view><text>随时为你待命</text></view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      capabilities: [
        { icon: '✦', title: '灵感与创作', description: '梳理想法，写出打动人的内容', color: 'purple' },
        { icon: '</>', title: '代码与产品', description: '分析问题，协作构建实用的功能', color: 'blue' },
        { icon: '↗', title: '学习与分析', description: '把复杂信息变成清晰的下一步', color: 'orange' }
      ],
      steps: [
        { title: '告诉我你的目标', description: '一句话、一个草稿，甚至一个模糊的念头都可以。' },
        { title: '一起探索方案', description: '我会提出思路、补全细节，并说明关键取舍。' },
        { title: '拿到可用结果', description: '获得可以继续推进的文本、计划、代码或答案。' }
      ]
    }
  },
  methods: {
    startChat() { uni.showToast({ title: '告诉我你想完成什么', icon: 'none' }) }
  }
}
</script>

<style>
page { background: #f6f7fb; }
.page { min-height: 100vh; padding: 68rpx 40rpx 48rpx; box-sizing: border-box; color: #202238; background: radial-gradient(circle at 96% 2%, #e8e7ff 0, rgba(232,231,255,0) 30%), #f6f7fb; }
.hero { padding: 18rpx 8rpx 70rpx; }.badge { display: inline-flex; align-items: center; padding: 12rpx 18rpx; border-radius: 999rpx; color: #5c55bd; background: #ecebff; font-size: 23rpx; letter-spacing: 1rpx; }.badge-dot { width: 12rpx; height: 12rpx; margin-right: 11rpx; border-radius: 50%; background: #6d63d9; box-shadow: 0 0 0 6rpx rgba(109,99,217,.14); }
.headline { display: block; margin-top: 34rpx; font-size: 64rpx; line-height: 1.22; font-weight: 700; letter-spacing: -3rpx; }.headline text { color: #665dd3; }.intro { display: block; margin-top: 26rpx; color: #777a90; font-size: 28rpx; line-height: 1.8; }.primary-button { width: 100%; height: 94rpx; margin-top: 38rpx; border: 0; border-radius: 24rpx; color: #fff; background: #5f58c9; box-shadow: 0 12rpx 24rpx rgba(95,88,201,.24); font-size: 29rpx; font-weight: 600; line-height: 94rpx; }.primary-button::after { border: 0; }.primary-button text { margin-left: 14rpx; font-size: 34rpx; }.hint { display: block; margin-top: 18rpx; color: #9b9daf; font-size: 23rpx; text-align: center; }
.section-head { margin-bottom: 24rpx; }.kicker { display: block; color: #7973cb; font-size: 22rpx; font-weight: 600; letter-spacing: 2rpx; }.section-title { display: block; margin-top: 11rpx; font-size: 35rpx; font-weight: 700; letter-spacing: -1rpx; }.cards { display: flex; flex-direction: column; gap: 18rpx; }.card { display: flex; align-items: center; min-height: 132rpx; padding: 22rpx; border: 1rpx solid #e6e6f0; border-radius: 24rpx; background: rgba(255,255,255,.92); box-sizing: border-box; }.icon { display: flex; flex: 0 0 76rpx; align-items: center; justify-content: center; width: 76rpx; height: 76rpx; margin-right: 21rpx; border-radius: 20rpx; font-size: 30rpx; font-weight: 700; }.purple { color: #6a5ed4; background: #efedff; }.blue { color: #4086c9; background: #eaf5ff; }.orange { color: #dd8c4a; background: #fff2e6; }.card-copy { flex: 1; }.card-title { display: block; font-size: 29rpx; font-weight: 600; }.card-desc { display: block; margin-top: 7rpx; color: #86899b; font-size: 23rpx; }.chevron { color: #b0b2c0; font-size: 42rpx; }
.workflow { margin-top: 54rpx; padding: 30rpx; border-radius: 28rpx; color: #f7f6ff; background: #282842; box-shadow: 0 18rpx 32rpx rgba(38,38,64,.18); }.workflow-head { display: flex; justify-content: space-between; padding-bottom: 24rpx; }.workflow .kicker { color: #aaa6ef; }.workflow-title { display: block; margin-top: 10rpx; font-size: 34rpx; font-weight: 650; }.sparkle { color: #b9b4ff; font-size: 43rpx; }.step { display: flex; padding: 24rpx 0; border-top: 1rpx solid rgba(255,255,255,.12); }.step-no { flex: 0 0 68rpx; color: #a9a4ec; font-size: 24rpx; font-weight: 700; }.step-title { display: block; font-size: 27rpx; font-weight: 600; }.step-desc { display: block; margin-top: 7rpx; color: #b6b6c7; font-size: 23rpx; line-height: 1.55; }.footer { display: flex; align-items: center; justify-content: center; margin-top: 46rpx; color: #a5a6b3; font-size: 21rpx; }.footer view { width: 6rpx; height: 6rpx; margin: 0 14rpx; border-radius: 50%; background: #aaa8c8; }
</style>
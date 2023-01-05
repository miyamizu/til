## ActiveJob

[公式ドキュメント](https://railsguides.jp/active_job_basics.html)
[ActiveJob の perform_later と perform_now の違い](https://qiita.com/jnchito/items/3482a30262874b80a8e4)

## Rspec

### description, context, it の使い分け

```
describe "#perform_later" do
  it 'キューに入ること' do
    subject
    expect(UpdateSapumonCoinJob).to have_been_enqueued
  end

  it 'retryable であること' do
    subject
    expect(UpdateSapumonCoinJob).to be_retryable true
  end
end

describe "#perform_now" do
  before { stub_request() }

  context 'qmonolith が 2XX系' do
    it 'jobが成功すること' do
    end
  end

  context 'qmonolith が 3XX-4XX系' do
    it 'Sentryにエラー送信すること' do
    end
  end

  context 'qmonolith が 5XX' do
    it '例外が発生すること' do
    end
  end
end
```

### stub

```
        stub_request(:post, "http://hoge-service")
          .to_return(
            status: 500,
            body: {}.to_json,
            headers: { 'Content-Type' => 'application/json' }
          ).with(
          body: {
            "user_id" => user.id,
          },
          headers: { 'Content-Type'=>'application/json' }
        )
      end
```

### mock

```
    before do
      allow(LaunchDarklyClient.client).to receive(:variation).with('keyの名前', anything, false).and_return(true)
    end
```

### 1 回メソッドが実行されたか

```
 expect(HogeJob).to have_received(:perform_later).once
 expect(UpdateSapumonCoinJob).not_to have_received(:perform_later)
```

### エラーがでたこと

```
expect { subject }.to raise_error(InternalServerError)
```

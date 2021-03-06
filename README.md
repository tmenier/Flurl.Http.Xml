# Flurl.Http.Xml
Extension for Flurl.Http to support XML

Usage:

    [TestFixture]
    public class RealHttpTests
    {
        [Test]
        public void GetXml()
        {
            var result = "https://query.yahooapis.com/v1/public/yql"
                .SetQueryParam("q", "select wind from weather.forecast where woeid=2460286")
                .SetQueryParam("format", "xml")
                .GetXmlAsync<YahooWeatherModels.Query>()
                .Result;

            Assert.IsNotNull(result);
            Assert.IsNotNullOrEmpty(result.Results.Channel.Wind.Chill);
        }

        [Test]
        public void PostXml()
        {
            var result = "http://httpbin.org/post".PostXmlAsync(new TestModel { Number = 3, Text = "Test" }).ReceiveXmlFromJsonAsync<TestModel>(json => json.data).Result;

            Assert.AreEqual(3, result.Number);
            Assert.AreEqual("Test", result.Text);
        }
    }


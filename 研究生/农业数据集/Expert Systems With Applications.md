1. Yeild data

   从美国农业统计局（USDA National Agricultural Statistical Services，NASS）的Quick Stat工具中收集了基于县级的大豆统计数据，该工具可在https://www.nass.usda.gov/Quick_Stats/index.php上获得。2003年至2019年的产量数据被用作模型训练的真实标签。

2. MODIS Surface reflectance

   MODIS/Terra表面反射（SR）产品提供了7个波段的表面光谱反射，空间分辨率为500米，每8天更新一次（Vermote, 2015）。每个像素点包含在8天窗口内从所有采集中选择的最佳SR观测值。该产品可在https://lpdaac.usgs.gov/products/mod09a1v006/公开获取。在这里，我们使用了版本6的该产品的全部7个波段进行大豆产量预测。

3. MODIS Land cover

   Terra和Aqua结合的MODIS土地覆盖类型（LC）产品提供了每年的土地覆盖类型，分辨率为500米，根据六种分类方案（Sulla-Menashe＆Friedl, 2019）进行推导。本研究使用了每年一次的马里兰大学（UMD）分类（土地覆盖类型2）方案来屏蔽农田区域。该数据集可在https://lpdaac.usgs.gov/products/mcd12q1v006/上公开获取。

4. MODIS Land Surface temperature

   MODIS第6版陆地表面温度（LST）提供了每像素8天的平均白天和夜间表面温度，空间分辨率为1公里（Wan, 2015）。通过使用7个热红外波段和LST算法收集温度数据（Wan, 2006）。该数据集已广泛应用于多种研究中（Abbaszadeh等，2021; Benali等，2012; Wang等，2021）。在本研究中，同时使用了白天和夜间的LST。该产品可在https://lpdaac.usgs.gov/products/myd11a2v006/上公开获取。
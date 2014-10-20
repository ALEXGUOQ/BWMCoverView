BWMCoverView
============

BWM出品的用于快速简便地创建UIScrollView和UIPageControl的图片展示封面，支持循环滚动，动画，异步加载图片等功能。

/**
     * 快速创建BWMCoverView
     * models是一个包含图片地址的数组
     * placeholderImageNamed为图片加载前的本地占位图片名
     */
    BWMCoverView *coverView = [BWMCoverView coverViewWithModels:realArray andFrame:CGRectMake(10, 50, 300, 400) andPlaceholderImageNamed:@"defaultImage" andClickdCallBlock:^(NSInteger index) {
        NSLog(@"你选择了第%d个图片", index);
    }];
    
    // 请打开下面的东西逐个调试
    // [coverView setAutoPlayWithDelay:3.0]; // 设置自动播放
    // [coverView stopAutoPlayWithBOOL:YES]; // 停止自动播放
    // [coverView stopAutoPlayWithBOOL:NO]; // 恢复开启自动播放
    // [coverView setAnimationOption:UIViewAnimationOptionTransitionCurlUp]; // 设置切换动画
    
    [self.view addSubview:coverView];

接口
 /**
 * BWM出品的用于创建UIScrollView和UIPageControl的图片展示封面
 * 支持循环滚动，动画，异步加载图片
 */
@interface BWMCoverView : UIView <UIScrollViewDelegate>

@property (nonatomic, strong) UIScrollView *scrollView;
@property (nonatomic, strong) UIPageControl *pageControl;
@property (nonatomic, strong) NSArray *models; // 一个包含图片地址字符串的数组
@property (nonatomic, copy) NSString *placeholderImageNamed; // 图片载入前的本地占位图片名字符串
@property (nonatomic, copy) void(^callBlock)(NSInteger); // 点击后的调用的block
@property (nonatomic, assign) UIViewAnimationOptions animationOption; // 动画选项（可选）

- (id)initWithModels:(NSArray *)models andFrame:(CGRect)frame;

/**
 * 快速创建BWMCoverView
 * @param models是一个包含图片地址的数组
 * @param placeholderImageNamed为图片加载前的本地占位图片名
 */
+ (id)coverViewWithModels:(NSArray *)models andFrame:(CGRect)frame andPlaceholderImageNamed:(NSString *)placeholderImageNamed andClickdCallBlock:(void (^)(NSInteger index))callBlock;


/** 如果用init创建BWMCoverView，则需要更新视图才能够正常使用 */
- (void)updateView;

/** 设置图片点击后的块回调 */
- (void)setCallBlock:(void (^)(NSInteger index))callBlock;

/** 设置自动播放 */
- (void)setAutoPlayWithDelay:(NSTimeInterval)second;

/** 停止或恢复自动播放（在设置了自动播放时才有效） */
- (void)stopAutoPlayWithBOOL:(BOOL)isStopAutoPlay;

/** 
 * 设置切换时的动画选项，不设置则默认为scrollView滚动动画
 * 提供的动画类型有：
 *   UIViewAnimationOptionTransitionNone
 *   UIViewAnimationOptionTransitionFlipFromLeft
 *   UIViewAnimationOptionTransitionFlipFromRight
 *   UIViewAnimationOptionTransitionCurlUp
 *   UIViewAnimationOptionTransitionCurlDown
 *   UIViewAnimationOptionTransitionCrossDissolve
 *   UIViewAnimationOptionTransitionFlipFromTop
 *   UIViewAnimationOptionTransitionFlipFromBottom
 */
- (void)setAnimationOption:(UIViewAnimationOptions)animationOption;
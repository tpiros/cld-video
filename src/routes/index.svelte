<script>
	let myCloudinary;

	const init = async () => {
		// grab products

		const source = {
			shoppable: {
				transformation: {
					crop: 'pad',
					aspect_ratio: '1'
				},
				products: [
					{
						productId: 1,
						productName: 'Jacket',
						startTime: 0,
						endTime: 10,
						publicId: 'docs/shoppable_sunglasses',
						hotspots: [
							{
								time: '00:02',
								x: '50%',
								y: '50%',
								tooltipPosition: 'left',
								clickUrl:
									'https://cloudinary.com/blog/get_interactive_with_cloudinary_s_shoppable_video_and_video_player'
							}
						],
						onHover: {
							action: 'overlay',
							args: 'Click to see this product in the video'
						},
						onClick: {
							action: 'seek',
							pause: 5,
							args: {
								time: '00:02'
							}
						}
					}
				]
			}
		};

		myCloudinary = window.cloudinary.Cloudinary.new({ cloud_name: 'tamas-demo' });
		const demoplayer = myCloudinary.videoPlayer('doc-player').width(600);
		demoplayer.source('colombia', source);
	};
</script>

<svelte:head>
	<link
		href="https://unpkg.com/cloudinary-video-player@1.5.9/dist/cld-video-player.min.css"
		rel="stylesheet"
	/>
	<script
		src="https://unpkg.com/cloudinary-core@latest/cloudinary-core-shrinkwrap.min.js"
		type="text/javascript"></script>
	<script
		src="https://unpkg.com/cloudinary-video-player@1.5.9/dist/cld-video-player.min.js"
		type="text/javascript"
		on:load={init}></script>
</svelte:head>

<h1>Products</h1>
<video id="doc-player" controls muted class="cld-video-player cld-fluid" />

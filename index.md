### Wordpress code for assets url

```markdown
<img src="<?php echo get_template_directory_uri(); ?>/assets/images/iphone.png">
```

### Show wordpress all categories in loop

```markdown
<?php
$cat_args=array(
	'orderby' => 'name',
	'order' => 'ASC'
	);
	$categories=get_categories($cat_args);
	foreach($categories as $category) { 
		$args=array(
			'category__in' => array($category->term_id),
			'caller_get_posts'=>1
			);
			$posts=get_posts($args);
			if ($posts) {

				echo '<div class="swiper-slide"><a href="' . get_category_link( $category->term_id ) . '" title="' . sprintf( __( "View all posts in %s" ), $category->name ) . '" ' . '>' . $category->name.'</a> </div> ';

				foreach($posts as $post) {
					setup_postdata($post); ?>
					<?php
				} 
			} 
		}
		?>
```

### Wordpress post loop

```markdown
<?php 
	query_posts(array( 
	'post_type' => 'post',
	'showposts' => 1 
	) );  
	?>
	<?php while (have_posts()) : the_post(); ?>				
	<!-- your content here -->
<?php endwhile;?>
```

### Show post views in wordpress

```markdown
<!-- Past code in functions.php file -->

function rm_post_view_count(){
	if ( is_single() ){
		global $post;
		$count_post = esc_attr( get_post_meta( $post->ID, '_post_views_count', true) );
		if( $count_post == ''){
			$count_post = 0;
			add_post_meta( $post->ID, '_post_views_count', $count_post);
		}else{
			$count_post = (int)$count_post + 0;
			update_post_meta( $post->ID, '_post_views_count', $count_post);
		}
	}
}
add_action('wp_head', 'rm_post_view_count');


<!-- Past code in single.php file -->

<?php 

if ( is_single() ){
		global $post;
		$count_post = esc_attr( get_post_meta( $post->ID, '_post_views_count', true) );
		if( $count_post == ''){
			$count_post = 1;
			add_post_meta( $post->ID, '_post_views_count', $count_post);
		}else{
			$count_post = (int)$count_post + 1;
			update_post_meta( $post->ID, '_post_views_count', $count_post);
		}
	}

	?>


<!-- Past code in post.php file -->

<?php
		global $post;
		$visitor_count = get_post_meta( $post->ID, '_post_views_count', true);
		if( $visitor_count == '' ){ $visitor_count = 0; }
		if( $visitor_count >= 1000 ){
			$visitor_count = round( ($visitor_count/1000), 1 );
			$visitor_count = $visitor_count.'k';
		}
	echo esc_attr($visitor_count);
?>	
```

### Wordpress simple post basic codes

```markdown
<article class="post">
		<div class="col-md-4">
			<div class="post-img" style="background: url('<?php echo get_the_post_thumbnail_url(); ?>');"></div>
			<a href="<?php echo get_permalink(); ?>" class="post-overlay">
				<img class="play-icon" src="<?php echo get_stylesheet_directory_uri(); ?>/assets/images/play.svg">
			</a>
			<div class="entry-content">
					<?php the_content(); ?>
				<a href="<?php echo get_permalink(); ?>"><h3 class="entry-title"><?php the_title(); ?></h3></a>
			</div>
		</div>
</article>
```

### Wordpress hide admin bar

```markdown
add_filter('show_admin_bar', '__return_false');
```

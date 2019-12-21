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
